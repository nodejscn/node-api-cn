<!-- YAML
added: v8.0.0
-->
```C
napi_status napi_unwrap(napi_env env,
                        napi_value js_object,
                        void** result);
```

 - `[in] env`: The environment that the API is invoked under.
 - `[in] js_object`: The object associated with the C++ class instance.
 - `[out] result`: Pointer to the wrapped C++ class instance.

Returns `napi_ok` if the API succeeded.

Retrieves a native instance that was previously wrapped in a JavaScript
object using `napi_wrap()`.

When JavaScript code invokes a method or property accessor on the class, the
corresponding `napi_callback` is invoked. If the callback is for an instance
method or accessor, then the `this` argument to the callback is the wrapper
object; the wrapped C++ instance that is the target of the call can be obtained
then by calling `napi_unwrap()` on the wrapper object.

