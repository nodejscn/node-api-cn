<!-- YAML
added: v8.0.0
napiVersion: 1
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
- `[in] typedarray`: `napi_value` representing the `TypedArray` whose
properties to query.
- `[out] type`: Scalar datatype of the elements within the `TypedArray`.
- `[out] length`: The number of elements in the `TypedArray`.
- `[out] data`: The data buffer underlying the `TypedArray` adjusted by
the `byte_offset` value so that it points to the first element in the
`TypedArray`.
- `[out] arraybuffer`: The `ArrayBuffer` underlying the `TypedArray`.
- `[out] byte_offset`: The byte offset within the underlying native array
at which the first element of the arrays is located. The value for the data
parameter has already been adjusted so that data points to the first element
in the array. Therefore, the first byte of the native array would be at
data - `byte_offset`.

Returns `napi_ok` if the API succeeded.

This API returns various properties of a typed array.

*Warning*: Use caution while using this API since the underlying data buffer
is managed by the VM.

