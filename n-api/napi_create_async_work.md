<!-- YAML
added: v8.0.0
changes:
  - version: v8.6.0
    pr-url: https://github.com/nodejs/node/pull/14697
    description: Added `async_resource` and `async_resource_name` parameters.
-->
```C
napi_status napi_create_async_work(napi_env env,
                                   napi_value async_resource,
                                   napi_value async_resource_name,
                                   napi_async_execute_callback execute,
                                   napi_async_complete_callback complete,
                                   void* data,
                                   napi_async_work* result);
```

- `[in] env`: The environment that the API is invoked under.
- `[in] async_resource`: An optional object associated with the async work
  that will be passed to possible async_hooks [`init` hooks][].
- `[in] async_resource_name`: An identifier for the kind of resource that is
being provided for diagnostic information exposed by the `async_hooks` API.
- `[in] execute`: The native function which should be called to excute
the logic asynchronously.
- `[in] complete`: The native function which will be called when the
asynchronous logic is comple or is cancelled.
- `[in] data`: User-provided data context. This will be passed back into the
execute and complete functions.
- `[out] result`: `napi_async_work*` which is the handle to the newly created
async work.

Returns `napi_ok` if the API succeeded.

This API allocates a work object that is used to execute logic asynchronously.
It should be freed using [`napi_delete_async_work`][] once the work is no longer
required.

`async_resource_name` should be a null-terminated, UTF-8-encoded string.

*Note*: The `async_resource_name` identifier is provided by the user and should
be representative of the type of async work being performed. It is also
recommended to apply namespacing to the identifier, e.g. by including the
module name. See the [`async_hooks` documentation][async_hooks `type`]
for more information.

