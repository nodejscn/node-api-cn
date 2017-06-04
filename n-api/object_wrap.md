
N-API offers a way to "wrap" C++ classes and instances so that the class
constructor and methods can be called from JavaScript.

 1. The [`napi_define_class`][] API defines a JavaScript class with constructor,
    static properties and methods, and instance properties and methods that
    correspond to the The C++ class.
 2. When JavaScript code invokes the constructor, the constructor callback
    uses [`napi_wrap`][] to wrap a new C++ instance in a JavaScript object,
    then returns the wrapper object.
 3. When JavaScript code invokes a method or property accessor on the class,
    the corresponding `napi_callback` C++ function is invoked. For an instance
    callback, [`napi_unwrap`][] obtains the C++ instance that is the target of
    the call.

