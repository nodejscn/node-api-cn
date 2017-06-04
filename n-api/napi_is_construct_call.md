<!-- YAML
added: v8.0.0
-->
```C
napi_status napi_is_construct_call(napi_env env,
                                   napi_callback_info cbinfo,
                                   bool* result)
```

- `[in] env`: The environment that the API is invoked under.
- `[in] cbinfo`: The callback info passed into the callback function.
- `[out] result`: Whether the native function is being invoked as
a constructor call.

Returns `napi_ok` if the API succeeded.

This API checks if the the current callback was due to a
consructor call.

