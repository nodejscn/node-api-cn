Function pointer used with functions that support asynchronous
operations. Callback functions must statisfy the following signature:

```C
typedef void (*napi_async_execute_callback)(napi_env env, void* data);
```

