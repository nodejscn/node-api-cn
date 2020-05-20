<!-- YAML
added: v8.6.0
napiVersion: 1
-->

```C
napi_status napi_async_init(napi_env env,
                            napi_value async_resource,
                            napi_value async_resource_name,
                            napi_async_context* result)
```

* `[in] env`: The environment that the API is invoked under.
* `[in] async_resource`: Object associated with the async work
  that will be passed to possible `async_hooks` [`init` hooks][].
  In order to retain ABI compatibility with previous versions,
  passing `NULL` for `async_resource` will not result in an error, however,
  this will result incorrect operation of async hooks for the
  napi_async_context created. Potential issues include
  loss of async context when using the AsyncLocalStorage API.
* `[in] async_resource_name`: Identifier for the kind of resource
  that is being provided for diagnostic information exposed by the
  `async_hooks` API.
* `[out] result`: The initialized async context.

Returns `napi_ok` if the API succeeded.

