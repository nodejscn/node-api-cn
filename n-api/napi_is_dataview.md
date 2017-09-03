<!-- YAML
added: v8.3.0
-->

```C
napi_status napi_is_dataview(napi_env env, napi_value value, bool* result)
```

- `[in] env`: The environment that the API is invoked under.
- `[in] value`: The JavaScript value to check.
- `[out] result`: Whether the given `napi_value` represents a DataView.

Returns `napi_ok` if the API succeeded.

This API checks if the Object passed in is a DataView.

