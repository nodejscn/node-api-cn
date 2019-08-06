<!-- YAML
added: v8.0.0
napiVersion: 1
-->
Function pointer used with functions that support asynchronous
operations. Callback functions must satisfy the following signature:

```C
typedef void (*napi_async_execute_callback)(napi_env env, void* data);
```

Implementations of this type of function should avoid making any N-API calls
that could result in the execution of JavaScript or interaction with
JavaScript objects. Most often, any code that needs to make N-API
calls should be made in `napi_async_complete_callback` instead.
Avoid using the `napi_env` parameter in the execute callback as
it will likely execute JavaScript.

