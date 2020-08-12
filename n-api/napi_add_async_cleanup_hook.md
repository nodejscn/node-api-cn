<!-- YAML
added: v14.8.0
-->

> Stability: 1 - Experimental

```c
NAPI_EXTERN napi_status napi_add_async_cleanup_hook(
    napi_env env,
    void (*fun)(void* arg, void(* cb)(void*), void* cbarg),
    void* arg,
    napi_async_cleanup_hook_handle* remove_handle);
```

Registers `fun` as a function to be run with the `arg` parameter once the
current Node.js environment exits. Unlike [`napi_add_env_cleanup_hook`][],
the hook is allowed to be asynchronous in this case, and must invoke the passed
`cb()` function with `cbarg` once all asynchronous activity is finished.

Otherwise, behavior generally matches that of [`napi_add_env_cleanup_hook`][].

If `remove_handle` is not `NULL`, an opaque value will be stored in it
that must later be passed to [`napi_remove_async_cleanup_hook`][],
regardless of whether the hook has already been invoked.
Typically, that happens when the resource for which this hook was added
is being torn down anyway.

