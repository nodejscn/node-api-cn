Function pointer used with functions that support asynchronous
operations. Callback functions must statisfy the following signature:

```C
typedef void (*napi_async_execute_callback)(napi_env env, void* data);
```

Implementations of this type of function should avoid making any N-API calls
that could result in the execution of JavaScript or interaction with
JavaScript objects. Most often, any code that needs to make N-API
calls should be made in `napi_async_complete_callback` instead.

