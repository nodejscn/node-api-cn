<!-- YAML
added: v8.0.0
-->
```C
NODE_EXTERN napi_status
    napi_open_escapable_handle_scope(napi_env env,
                                     napi_handle_scope* result);
```
- `[in] env`: The environment that the API is invoked under.
- `[out] result`: `napi_value` representing the new scope.

Returns `napi_ok` if the API succeeded.

This API open a new scope from which one object can be promoted
to the outer scope.

