<!-- YAML
added: v14.8.0
changes:
  - version: v14.10.0
    pr-url: https://github.com/nodejs/node/pull/34819
    description: Changed signature of the `hook` callback.
-->

> Stability: 1 - Experimental

```c
NAPI_EXTERN napi_status napi_add_async_cleanup_hook(
    napi_env env,
    napi_async_cleanup_hook hook,
    void* arg,
    napi_async_cleanup_hook_handle* remove_handle);
```

* `[in] env`: The environment that the API is invoked under.
* `[in] hook`: The function pointer to call at environment teardown.
* `[in] arg`: The pointer to pass to `hook` when it gets called.
* `[out] remove_handle`: Optional handle that refers to the asynchronous cleanup
hook.

Registers `hook`, which is a function of type [`napi_async_cleanup_hook`][], as
a function to be run with the `remove_handle` and `arg` parameters once the
current Node.js environment exits.

Unlike [`napi_add_env_cleanup_hook`][], the hook is allowed to be asynchronous.

Otherwise, behavior generally matches that of [`napi_add_env_cleanup_hook`][].

If `remove_handle` is not `NULL`, an opaque value will be stored in it
that must later be passed to [`napi_remove_async_cleanup_hook`][],
regardless of whether the hook has already been invoked.
Typically, that happens when the resource for which this hook was added
is being torn down anyway.

