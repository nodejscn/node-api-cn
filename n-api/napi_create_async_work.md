<!-- YAML
added: v8.0.0
-->
```C
NAPI_EXTERN
napi_status napi_create_async_work(napi_env env,
                                   napi_async_execute_callback execute,
                                   napi_async_complete_callback complete,
                                   void* data,
                                   napi_async_work* result);
```

- `[in] env`: The environment that the API is invoked under.
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

