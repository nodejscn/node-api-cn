<!-- YAML
added: v8.6.0
-->
```C
napi_status napi_async_init(napi_env env,
                            napi_value async_resource,
                            napi_value async_resource_name,
                            napi_async_context* result)
```

- `[in] env`: The environment that the API is invoked under.
- `[in] async_resource`: An optional object associated with the async work
  that will be passed to possible `async_hooks` [`init` hooks][].
- `[in] async_resource_name`: Required identifier for the kind of resource
  that is being provided for diagnostic information exposed by the
  `async_hooks` API.
- `[out] result`: The initialized async context.

Returns `napi_ok` if the API succeeded.

