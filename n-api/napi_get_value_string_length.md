<!-- YAML
added: v8.0.0
-->
```C
napi_status napi_get_value_string_length(napi_env env,
                                         napi_value value,
                                         int* result)
```

- `[in] env`: The environment that the API is invoked under.
- `[in] value`: `napi_value` representing JavaScript string.
- `[out] result`: Number of characters in the given JavaScript string.

Returns `napi_ok` if the API succeeded. If a non-String `napi_value`
is passed in it returns `napi_string_expected`.

This API returns the number of characters in the given JavaScript string.

