<!-- YAML
added: v8.0.0
-->
```C
napi_status napi_get_null(napi_env env, napi_value* result)
```

- `[in] env`: The environment that the API is invoked under.
- `[out] result`: `napi_value` representing JavaScript Null Object.

Returns `napi_ok` if the API succeeded.

This API returns the null Object.

