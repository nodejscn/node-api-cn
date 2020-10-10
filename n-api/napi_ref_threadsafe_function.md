
<!-- YAML
added: v10.6.0
napiVersion: 4
-->

```c
NAPI_EXTERN napi_status
napi_ref_threadsafe_function(napi_env env, napi_threadsafe_function func);
```

* `[in] env`: The environment that the API is invoked under.
* `[in] func`: The thread-safe function to reference.

This API is used to indicate that the event loop running on the main thread
should not exit until `func` has been destroyed. Similar to [`uv_ref`][] it is
also idempotent.

Neither does `napi_unref_threadsafe_function` mark the thread-safe functions as
able to be destroyed nor does `napi_ref_threadsafe_function` prevent it from
being destroyed. `napi_acquire_threadsafe_function` and
`napi_release_threadsafe_function` are available for that purpose.

This API may only be called from the main thread.

