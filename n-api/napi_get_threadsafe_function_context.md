
<!-- YAML
added: v10.6.0
napiVersion: 4
-->
```C
NAPI_EXTERN napi_status
napi_get_threadsafe_function_context(napi_threadsafe_function func,
                                     void** result);
```

- `[in] func`: The thread-safe function for which to retrieve the context.
- `[out] result`: The location where to store the context.

This API may be called from any thread which makes use of `func`.

