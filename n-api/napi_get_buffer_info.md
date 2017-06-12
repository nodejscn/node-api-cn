<!-- YAML
added: v8.0.0
-->
```C
napi_status napi_get_buffer_info(napi_env env,
                                 napi_value value,
                                 void** data,
                                 size_t* length)
```

- `[in] env`: The environment that the API is invoked under.
- `[in] value`: `napi_value` representing the `node::Buffer` being queried.
- `[out] data`: The underlying data buffer of the `node::Buffer`.
- `[out] length`: Length in bytes of the underlying data buffer.

Returns `napi_ok` if the API succeeded.

This API is used to retrieve the underlying data buffer of a `node::Buffer`
and it's length.

*Warning*: Use caution while using this API since the underlying data buffer's
lifetime is not guaranteed if it's managed by the VM.

