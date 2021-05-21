<!-- YAML
added: v8.0.0
napiVersion: 1
-->
Function pointer type for user-provided native functions which are to be
exposed to JavaScript via Node-API. Callback functions should satisfy the
following signature:

```c
typedef napi_value (*napi_callback)(napi_env, napi_callback_info);
```

Unless for reasons discussed in [Object Lifetime Management][], creating a
handle and/or callback scope inside a `napi_callback` is not necessary.

