<!-- YAML
added: v9.6.0
-->
```C
NAPI_EXTERN napi_status napi_close_callback_scope(napi_env env,
                                                  napi_callback_scope scope)
```
- `[in] env`: The environment that the API is invoked under.
- `[in] scope`: The scope to be closed.

This API can be called even if there is a pending JavaScript exception.

