<!-- YAML
added: v8.0.0
-->
```C
napi_status napi_get_typedarray_info(napi_env env,
                                     napi_value typedarray,
                                     napi_typedarray_type* type,
                                     size_t* length,
                                     void** data,
                                     napi_value* arraybuffer,
                                     size_t* byte_offset)
```

- `[in] env`: The environment that the API is invoked under.
- `[in] typedarray`: `napi_value` representing the TypedArray whose
properties to query.
- `[out] type`: Scalar datatype of the elements within the TypedArray.
- `[out] length`: Number of elements in the TypedArray.
- `[out] data`: The data buffer underlying the typed array.
- `[out] byte_offset`: The byte offset within the data buffer from which
to start projecting the TypedArray.

Returns `napi_ok` if the API succeeded.

This API returns various properties of a typed array.

*Warning*: Use caution while using this API since the underlying data buffer
is managed by the VM



