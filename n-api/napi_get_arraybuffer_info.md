<!-- YAML
added: v8.0.0
-->
```C
napi_status napi_get_arraybuffer_info(napi_env env,
                                      napi_value arraybuffer,
                                      void** data,
                                      size_t* byte_length)
```

- `[in] env`: The environment that the API is invoked under.
- `[in] arraybuffer`: `napi_value` representing the ArrayBuffer being queried.
- `[out] data`: The underlying data buffer of the ArrayBuffer.
- `[out] byte_length`: Length in bytes of the underlying data buffer.

Returns `napi_ok` if the API succeeded.

This API is used to retrieve the underlying data buffer of an ArrayBuffer and
its length.

*WARNING*: Use caution while using this API. The lifetime of the underlying data
buffer is managed by the ArrayBuffer even after it's returned. A
possible safe way to use this API is in conjunction with [`napi_create_reference`][],
which can be used to guarantee control over the lifetime of the
ArrayBuffer. It's also safe to use the returned data buffer within the same
callback as long as there are no calls to other APIs that might trigger a GC.

