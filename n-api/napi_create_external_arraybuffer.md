<!-- YAML
added: v8.0.0
-->
```C
napi_status
napi_create_external_arraybuffer(napi_env env,
                                 void* external_data,
                                 size_t byte_length,
                                 napi_finalize finalize_cb,
                                 void* finalize_hint,
                                 napi_value* result)
```

- `[in] env`: The environment that the API is invoked under.
- `[in] external_data`: Pointer to the underlying byte buffer of the
ArrayBuffer.
- `[in] byte_length`: The length in bytes of the underlying buffer.
- `[in] finalize_cb`: Optional callback to call when the ArrayBuffer is
being collected.
- `[in] finalize_hint`: Optional hint to pass to the finalize callback
during collection.
- `[out] result`: A `napi_value` representing a JavaScript ArrayBuffer.

Returns `napi_ok` if the API succeeded.

This API returns an N-API value corresponding to a JavaScript ArrayBuffer.
The underlying byte buffer of the ArrayBuffer is externally allocated and
managed. The caller must ensure that the byte buffer remains valid until the
finalize callback is called.

JavaScript ArrayBuffers are described in
[Section 24.1](https://tc39.github.io/ecma262/#sec-arraybuffer-objects)
of the ECMAScript Language Specification.

