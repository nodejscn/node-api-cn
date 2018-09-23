<!-- YAML
added: v8.0.0
napiVersion: 1
-->
```C
napi_status napi_create_function(napi_env env,
                                 const char* utf8name,
                                 size_t length,
                                 napi_callback cb,
                                 void* data,
                                 napi_value* result);
```

- `[in] env`: The environment that the API is invoked under.
- `[in] utf8Name`: The name of the function encoded as UTF8. This is visible
within JavaScript as the new function object's `name` property.
- `[in] length`: The length of the `utf8name` in bytes, or
`NAPI_AUTO_LENGTH` if it is null-terminated.
- `[in] cb`: The native function which should be called when this function
object is invoked.
- `[in] data`: User-provided data context. This will be passed back into the
function when invoked later.
- `[out] result`: `napi_value` representing the JavaScript function object for
the newly created function.

Returns `napi_ok` if the API succeeded.

This API allows an add-on author to create a function object in native code.
This is the primary mechanism to allow calling *into* the add-on's native code
*from* JavaScript.

The newly created function is not automatically visible from script after this
call. Instead, a property must be explicitly set on any object that is visible
to JavaScript, in order for the function to be accessible from script.

In order to expose a function as part of the
add-on's module exports, set the newly created function on the exports
object. A sample module might look as follows:
```C
napi_value SayHello(napi_env env, napi_callback_info info) {
  printf("Hello\n");
  return NULL;
}

napi_value Init(napi_env env, napi_value exports) {
  napi_status status;

  napi_value fn;
  status = napi_create_function(env, NULL, 0, SayHello, NULL, &fn);
  if (status != napi_ok) return NULL;

  status = napi_set_named_property(env, exports, "sayHello", fn);
  if (status != napi_ok) return NULL;

  return exports;
}

NAPI_MODULE(NODE_GYP_MODULE_NAME, Init)
```

Given the above code, the add-on can be used from JavaScript as follows:
```js
const myaddon = require('./addon');
myaddon.sayHello();
```

The string passed to `require()` is the name of the target in `binding.gyp`
responsible for creating the `.node` file.

Any non-`NULL` data which is passed to this API via the `data` parameter can
be associated with the resulting JavaScript function (which is returned in the
`result` parameter) and freed whenever the function is garbage-collected by
passing both the JavaScript function and the data to [`napi_add_finalizer`][].

JavaScript `Function`s are described in

of the ECMAScript Language Specification.

