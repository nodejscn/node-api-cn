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
- `[in] data`: Raw pointer to the external data.
- `[in] finalize_cb`: Optional callback to call when the external value
is being collected.
- `[in] finalize_hint`: Optional hint to pass to the finalize callback
during collection.
- `[out] result`: A `napi_value` representing an external value.

Returns `napi_ok` if the API succeeded.

This API allocates a JavaScript value with external data attached to it. This
is used to pass external data through JavaScript code, so it can be retrieved
later by native code. The API allows the caller to pass in a finalize callback,
in case the underlying native resource needs to be cleaned up when the external
JavaScript value gets collected.

*Note*: The created value is not an object, and therefore does not support
additional properties. It is considered a distinct value type: calling
`napi_typeof()` with an external value yields `napi_external`.

