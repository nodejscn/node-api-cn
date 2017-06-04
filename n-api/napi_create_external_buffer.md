<!-- YAML
added: v8.0.0
-->
```C
napi_status napi_create_external_buffer(napi_env env,
                                        size_t length,
                                        void* data,
                                        napi_finalize finalize_cb,
                                        void* finalize_hint,
                                        napi_value* result)
```

- `[in] env`: The environment that the API is invoked under.
- `[in] length`: Size in bytes of the input buffer (should be the same as
the size of the new buffer).
- `[in] data`: Raw pointer to the underlying buffer to copy from.
- `[in] finalize_cb`: Optional callback to call when the ArrayBuffer is
being collected.
- `[in] finalize_hint`: Optional hint to pass to the finalize callback
during collection.
- `[out] result`: A `napi_value` representing a `node::Buffer`.

Returns `napi_ok` if the API succeeded.

This API allocates a `node::Buffer` object and initializes it with data
backed by the passed in buffer. While this is still a fully-supported data
structure, in most cases using a TypedArray will suffice.

*Note*: For Node.js >=4 `Buffers` are Uint8Arrays.

