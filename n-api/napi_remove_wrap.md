<!-- YAML
added: v8.5.0
-->
```C
napi_status napi_remove_wrap(napi_env env,
                             napi_value js_object,
                             void** result);
```

 - `[in] env`: The environment that the API is invoked under.
 - `[in] js_object`: The object associated with the native instance.
 - `[out] result`: Pointer to the wrapped native instance.

Returns `napi_ok` if the API succeeded.

Retrieves a native instance that was previously wrapped in the JavaScript
object `js_object` using `napi_wrap()` and removes the wrapping, thereby
restoring the JavaScript object's prototype chain. If a finalize callback was
associated with the wrapping, it will no longer be called when the JavaScript
object becomes garbage-collected.

