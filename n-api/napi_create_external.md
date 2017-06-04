<!-- YAML
added: v8.0.0
-->
```C
napi_status napi_create_external(napi_env env,
                                 void* data,
                                 napi_finalize finalize_cb,
                                 void* finalize_hint,
                                 napi_value* result)
```

- `[in] env`: The environment that the API is invoked under.
- `[in] data`: Raw pointer to the external data being wrapped.
- `[in] finalize_cb`: Optional callback to call when the wrapped object
is being collected.
- `[in] finalize_hint`: Optional hint to pass to the finalize callback
during collection.
- `[out] result`: A `napi_value` representing an external object.

Returns `napi_ok` if the API succeeded.

This API allocates a JavaScript object with external data attached to it.
This is used to wrap native objects and project them into JavaScript.
The API allows the caller to pass in a finalize callback, in case the
underlying native resource needs to be cleaned up when the wrapper
JavaScript object gets collected.

