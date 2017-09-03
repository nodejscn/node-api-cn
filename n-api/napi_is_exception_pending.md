<!-- YAML
added: v8.0.0
-->
```C
NAPI_EXTERN napi_status napi_is_exception_pending(napi_env env, bool* result);
```

- `[in] env`: The environment that the API is invoked under.
- `[out] result`: Boolean value that is set to true if an exception is pending.

Returns `napi_ok` if the API succeeded.

This API returns true if an exception is pending.

