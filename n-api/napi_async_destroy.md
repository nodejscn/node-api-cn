<!-- YAML
added: v8.6.0
-->
```C
napi_status napi_async_destroy(napi_env env,
                               napi_async_context async_context);
```

- `[in] env`: The environment that the API is invoked under.
- `[in] async_context`: The async context to be destroyed.

Returns `napi_ok` if the API succeeded.

