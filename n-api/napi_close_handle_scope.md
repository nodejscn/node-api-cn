<!-- YAML
added: v8.0.0
-->
```C
NAPI_EXTERN napi_status napi_close_handle_scope(napi_env env,
                                                napi_handle_scope scope);
```
- `[in] env`: The environment that the API is invoked under.
- `[in] scope`: `napi_value` representing the scope to be closed.

Returns `napi_ok` if the API succeeded.

This API closes the scope passed in. Scopes must be closed in the
reverse order from which they were created.

This API can be called even if there is a pending JavaScript exception.

