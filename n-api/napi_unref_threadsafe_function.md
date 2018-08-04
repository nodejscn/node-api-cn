
> Stability: 1 - Experimental

<!-- YAML
added: v10.6.0
-->
```C
NAPI_EXTERN napi_status
napi_unref_threadsafe_function(napi_env env, napi_threadsafe_function func);
```

- `[in] env`: The environment that the API is invoked under.
- `[in] func`: The thread-safe function to unreference.

This API is used to indicate that the event loop running on the main thread
may exit before `func` is destroyed. Similar to [`uv_unref`][] it is also
idempotent.

This API may only be called from the main thread.






































































