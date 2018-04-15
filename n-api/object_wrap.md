
N-API offers a way to "wrap" C++ classes and instances so that the class
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

As an example:

```C
napi_value MyClass_constructor = nullptr;
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

