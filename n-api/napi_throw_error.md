<!-- YAML
added: v8.0.0
-->
```C
NODE_EXTERN napi_status napi_throw_error(napi_env env,
                                         const char* code,
                                         const char* msg);
```
- `[in] env`: The environment that the API is invoked under.
- `[in] code`: Optional error code to be set on the error.
- `[in] msg`: C string representing the text to be associated with
the error.

Returns `napi_ok` if the API succeeded.

This API throws a JavaScript Error with the text provided.

