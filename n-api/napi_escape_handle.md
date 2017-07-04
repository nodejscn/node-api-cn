<!-- YAML
added: v8.0.0
-->
```C
NAPI_EXTERN napi_status napi_escape_handle(napi_env env,
                                           napi_escapable_handle_scope scope,
                                           napi_value escapee,
                                           napi_value* result);
```

- `[in] env`: The environment that the API is invoked under.
- `[in] scope`: `napi_value` representing the current scope.
- `[in] escapee`: `napi_value` representing the JavaScript Object to be escaped.
- `[out] result`: `napi_value` representing the handle to the escaped
Object in the outer scope.

Returns `napi_ok` if the API succeeded.

This API promotes the handle to the JavaScript object so that it is valid
for the lifetime of the outer scope. It can only be called once per scope.
If it is called more than once an error will be returned.

