<!-- YAML
added: v8.0.0
napiVersion: 1
-->
Function pointer used with functions that support asynchronous
operations. Callback functions must satisfy the following signature:

```C
typedef void (*napi_async_complete_callback)(napi_env env,
                                             napi_status status,
                                             void* data);
```

