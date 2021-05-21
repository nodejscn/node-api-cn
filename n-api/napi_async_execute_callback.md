<!-- YAML
added: v8.0.0
napiVersion: 1
-->
Function pointer used with functions that support asynchronous
operations. Callback functions must satisfy the following signature:

```c
typedef void (*napi_async_execute_callback)(napi_env env, void* data);
```

Implementations of this function must avoid making Node-API calls that execute
JavaScript or interact with JavaScript objects. Node-API calls should be in the
`napi_async_complete_callback` instead. Do not use the `napi_env` parameter as
it will likely result in execution of JavaScript.

