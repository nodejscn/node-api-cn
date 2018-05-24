<!-- YAML
added: v8.0.0
-->
```C
NAPI_EXTERN napi_status napi_throw(napi_env env, napi_value error);
```
- `[in] env`: The environment that the API is invoked under.
- `[in] error`: The JavaScript value to be thrown.

Returns `napi_ok` if the API succeeded.

This API throws the JavaScript value provided.

