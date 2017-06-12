<!-- YAML
added: v8.0.0
-->
```C
napi_status napi_get_value_bool(napi_env env, napi_value value, bool* result)
```

- `[in] env`: The environment that the API is invoked under.
- `[in] value`: `napi_value` representing JavaScript Boolean.
- `[out] result`: C boolean primitive equivalent of the given JavaScript
Boolean.

Returns `napi_ok` if the API succeeded. If a non-boolean `napi_value` is
passed in it returns `napi_boolean_expected`.

This API returns the C boolean primitive equivalent of the given JavaScript
Boolean.

