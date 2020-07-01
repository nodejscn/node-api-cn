<!-- YAML
added: v10.2.0
napiVersion: 3
-->

```c
NAPI_EXTERN napi_status napi_remove_env_cleanup_hook(napi_env env,
                                                     void (*fun)(void* arg),
                                                     void* arg);
```

Unregisters `fun` as a function to be run with the `arg` parameter once the
current Node.js environment exits. Both the argument and the function value
need to be exact matches.

The function must have originally been registered
with `napi_add_env_cleanup_hook`, otherwise the process will abort.

