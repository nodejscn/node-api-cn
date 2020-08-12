<!-- YAML
added: v10.2.0
napiVersion: 3
-->

```c
NODE_EXTERN napi_status napi_add_env_cleanup_hook(napi_env env,
                                                  void (*fun)(void* arg),
                                                  void* arg);
```

Registers `fun` as a function to be run with the `arg` parameter once the
current Node.js environment exits.

A function can safely be specified multiple times with different
`arg` values. In that case, it will be called multiple times as well.
Providing the same `fun` and `arg` values multiple times is not allowed
and will lead the process to abort.

The hooks will be called in reverse order, i.e. the most recently added one
will be called first.

Removing this hook can be done by using [`napi_remove_env_cleanup_hook`][].
Typically, that happens when the resource for which this hook was added
is being torn down anyway.

For asynchronous cleanup, [`napi_add_async_cleanup_hook`][] is available.

