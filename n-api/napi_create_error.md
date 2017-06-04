<!-- YAML
added: v8.0.0
-->
```C
NODE_EXTERN napi_status napi_create_error(napi_env env, const char* msg);
```
- `[in] env`: The environment that the API is invoked under.
- `[in] msg`: C string representing the text to be associated with.
- `[out] result`: `napi_value` representing the error created.

Returns `napi_ok` if the API succeeded.

This API returns a JavaScript Error with the text provided.

