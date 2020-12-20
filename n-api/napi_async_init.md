<!-- YAML
added: v8.6.0
napiVersion: 1
-->

```c
napi_status napi_async_init(napi_env env,
                            napi_value async_resource,
                            napi_value async_resource_name,
                            napi_async_context* result)
```

* `[in] env`: The environment that the API is invoked under.
* `[in] async_resource`: Object associated with the async work
  that will be passed to possible `async_hooks` [`init` hooks][] and can be
  accessed by [`async_hooks.executionAsyncResource()`][].
* `[in] async_resource_name`: Identifier for the kind of resource that is being
  provided for diagnostic information exposed by the `async_hooks` API.
* `[out] result`: The initialized async context.

Returns `napi_ok` if the API succeeded.

The `async_resource` object needs to be kept alive until
[`napi_async_destroy`][] to keep `async_hooks` related API acts correctly. In
order to retain ABI compatibility with previous versions, `napi_async_context`s
are not maintaining the strong reference to the `async_resource` objects to
avoid introducing causing memory leaks. However, if the `async_resource` is
garbage collected by JavaScript engine before the `napi_async_context` was
destroyed by `napi_async_destroy`, calling `napi_async_context` related APIs
like [`napi_open_callback_scope`][] and [`napi_make_callback`][] can cause
problems like loss of async context when using the `AsyncLocalStoage` API.

In order to retain ABI compatibility with previous versions, passing `NULL`
for `async_resource` does not result in an error. However, this is not
recommended as this will result poor results with  `async_hooks`
[`init` hooks][] and `async_hooks.executionAsyncResource()` as the resource is
now required by the underlying `async_hooks` implementation in order to provide
the linkage between async callbacks.

