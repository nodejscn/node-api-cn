<!-- YAML
added: v8.0.0
napiVersion: 1
-->
```C
napi_status napi_queue_async_work(napi_env env,
                                  napi_async_work work);
```

- `[in] env`: The environment that the API is invoked under.
- `[in] work`: The handle returned by the call to `napi_create_async_work`.

Returns `napi_ok` if the API succeeded.

This API requests that the previously allocated work be scheduled
for execution. Once it returns successfully, this API must not be called again
with the same `napi_async_work` item or the result will be undefined.

