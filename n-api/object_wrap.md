
Node-API offers a way to "wrap" C++ classes and instances so that the class
constructor and methods can be called from JavaScript.

1. The [`napi_define_class`][] API defines a JavaScript class with constructor,
    static properties and methods, and instance properties and methods that
    correspond to the C++ class.
2. When JavaScript code invokes the constructor, the constructor callback
    uses [`napi_wrap`][] to wrap a new C++ instance in a JavaScript object,
    then returns the wrapper object.
3. When JavaScript code invokes a method or property accessor on the class,
    the corresponding `napi_callback` C++ function is invoked. For an instance
    callback, [`napi_unwrap`][] obtains the C++ instance that is the target of
    the call.

For wrapped objects it may be difficult to distinguish between a function
called on a class prototype and a function called on an instance of a class.
A common pattern used to address this problem is to save a persistent
reference to the class constructor for later `instanceof` checks.

```c
napi_value MyClass_constructor = NULL;
status = napi_get_reference_value(env, MyClass::es_constructor, &MyClass_constructor);
assert(napi_ok == status);
bool is_instance = false;
status = napi_instanceof(env, es_this, MyClass_constructor, &is_instance);
assert(napi_ok == status);
if (is_instance) {
  // napi_unwrap() ...
} else {
  // otherwise...
}
```

The reference must be freed once it is no longer needed.

There are occasions where `napi_instanceof()` is insufficient for ensuring that
a JavaScript object is a wrapper for a certain native type. This is the case
especially when wrapped JavaScript objects are passed back into the addon via
static methods rather than as the `this` value of prototype methods. In such
cases there is a chance that they may be unwrapped incorrectly.

```js
const myAddon = require('./build/Release/my_addon.node');

// `openDatabase()` returns a JavaScript object that wraps a native database
// handle.
const dbHandle = myAddon.openDatabase();

// `query()` returns a JavaScript object that wraps a native query handle.
const queryHandle = myAddon.query(dbHandle, 'Gimme ALL the things!');

// There is an accidental error in the line below. The first parameter to
// `myAddon.queryHasRecords()` should be the database handle (`dbHandle`), not
// the query handle (`query`), so the correct condition for the while-loop
// should be
//
// myAddon.queryHasRecords(dbHandle, queryHandle)
//
while (myAddon.queryHasRecords(queryHandle, dbHandle)) {
  // retrieve records
}
```

In the above example `myAddon.queryHasRecords()` is a method that accepts two
arguments. The first is a database handle and the second is a query handle.
Internally, it unwraps the first argument and casts the resulting pointer to a
native database handle. It then unwraps the second argument and casts the
resulting pointer to a query handle. If the arguments are passed in the wrong
order, the casts will work, however, there is a good chance that the underlying
database operation will fail, or will even cause an invalid memory access.

To ensure that the pointer retrieved from the first argument is indeed a pointer
to a database handle and, similarly, that the pointer retrieved from the second
argument is indeed a pointer to a query handle, the implementation of
`queryHasRecords()` has to perform a type validation. Retaining the JavaScript
class constructor from which the database handle was instantiated and the
constructor from which the query handle was instantiated in `napi_ref`s can
help, because `napi_instanceof()` can then be used to ensure that the instances
passed into `queryHashRecords()` are indeed of the correct type.

Unfortunately, `napi_instanceof()` does not protect against prototype
manipulation. For example, the prototype of the database handle instance can be
set to the prototype of the constructor for query handle instances. In this
case, the database handle instance can appear as a query handle instance, and it
will pass the `napi_instanceof()` test for a query handle instance, while still
containing a pointer to a database handle.

To this end, Node-API provides type-tagging capabilities.

A type tag is a 128-bit integer unique to the addon. Node-API provides the
`napi_type_tag` structure for storing a type tag. When such a value is passed
along with a JavaScript object stored in a `napi_value` to
`napi_type_tag_object()`, the JavaScript object will be "marked" with the
type tag. The "mark" is invisible on the JavaScript side. When a JavaScript
object arrives into a native binding, `napi_check_object_type_tag()` can be used
along with the original type tag to determine whether the JavaScript object was
previously "marked" with the type tag. This creates a type-checking capability
of a higher fidelity than `napi_instanceof()` can provide, because such type-
tagging survives prototype manipulation and addon unloading/reloading.

Continuing the above example, the following skeleton addon implementation
illustrates the use of `napi_type_tag_object()` and
`napi_check_object_type_tag()`.

```c
// This value is the type tag for a database handle. The command
//
//   uuidgen | sed -r -e 's/-//g' -e 's/(.{16})(.*)/0x\1, 0x\2/'
//
// can be used to obtain the two values with which to initialize the structure.
static const napi_type_tag DatabaseHandleTypeTag = {
  0x1edf75a38336451d, 0xa5ed9ce2e4c00c38
};

// This value is the type tag for a query handle.
static const napi_type_tag QueryHandleTypeTag = {
  0x9c73317f9fad44a3, 0x93c3920bf3b0ad6a
};

static napi_value
openDatabase(napi_env env, napi_callback_info info) {
  napi_status status;
  napi_value result;

  // Perform the underlying action which results in a database handle.
  DatabaseHandle* dbHandle = open_database();

  // Create a new, empty JS object.
  status = napi_create_object(env, &result);
  if (status != napi_ok) return NULL;

  // Tag the object to indicate that it holds a pointer to a `DatabaseHandle`.
  status = napi_type_tag_object(env, result, &DatabaseHandleTypeTag);
  if (status != napi_ok) return NULL;

  // Store the pointer to the `DatabaseHandle` structure inside the JS object.
  status = napi_wrap(env, result, dbHandle, NULL, NULL, NULL);
  if (status != napi_ok) return NULL;

  return result;
}

// Later when we receive a JavaScript object purporting to be a database handle
// we can use `napi_check_object_type_tag()` to ensure that it is indeed such a
// handle.

static napi_value
query(napi_env env, napi_callback_info info) {
  napi_status status;
  size_t argc = 2;
  napi_value argv[2];
  bool is_db_handle;

  status = napi_get_cb_info(env, info, &argc, argv, NULL, NULL);
  if (status != napi_ok) return NULL;

  // Check that the object passed as the first parameter has the previously
  // applied tag.
  status = napi_check_object_type_tag(env,
                                      argv[0],
                                      &DatabaseHandleTypeTag,
                                      &is_db_handle);
  if (status != napi_ok) return NULL;

  // Throw a `TypeError` if it doesn't.
  if (!is_db_handle) {
    // Throw a TypeError.
    return NULL;
  }
}
```

