<!-- YAML
added: v8.2.0
-->
```C
napi_status napi_delete_property(napi_env env,
                                 napi_value object,
                                 napi_value key,
                                 bool* result);
```

- `[in] env`: The environment that the N-API call is invoked under.
- `[in] object`: The object to query.
- `[in] key`: The name of the property to delete.
- `[out] result`: Whether the property deletion succeeded or not. `result` can
optionally be ignored by passing `NULL`.

Returns `napi_ok` if the API succeeded.

This API attempts to delete the `key` own property from `object`.


