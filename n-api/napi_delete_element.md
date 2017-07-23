<!-- YAML
added: v8.2.0
-->
```C
napi_status napi_delete_element(napi_env env,
                                napi_value object,
                                uint32_t index,
                                bool* result);
```

- `[in] env`: The environment that the N-API call is invoked under.
- `[in] object`: The object to query.
- `[in] index`: The index of the property to delete.
- `[out] result`: Whether the element deletion succeeded or not. `result` can
optionally be ignored by passing `NULL`.

Returns `napi_ok` if the API succeeded.

This API attempts to delete the specified `index` from `object`.

