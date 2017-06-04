<!-- YAML
added: v8.0.0
-->
```C
NAPI_EXTERN napi_status napi_get_and_clear_last_exception(napi_env env,
                                                          napi_value* result);
```

- `[in] env`: The environment that the API is invoked under.
- `[out] result`: The exception if one is pending, NULL otherwise.

Returns `napi_ok` if the API succeeded.

This API returns true if an exception is pending.

