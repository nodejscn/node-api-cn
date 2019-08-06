
<!-- YAML
added: v10.6.0
napiVersion: 4
-->
```C
NAPI_EXTERN napi_status
napi_ref_threadsafe_function(napi_env env, napi_threadsafe_function func);
```

- `[in] env`: The environment that the API is invoked under.
- `[in] func`: The thread-safe function to reference.

This API is used to indicate that the event loop running on the main thread
should not exit until `func` has been destroyed. Similar to [`uv_ref`][] it is
also idempotent.

This API may only be called from the main thread.

