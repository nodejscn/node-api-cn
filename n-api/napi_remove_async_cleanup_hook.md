<!-- YAML
added: v14.8.0
-->

> Stability: 1 - Experimental

```c
NAPI_EXTERN napi_status napi_remove_async_cleanup_hook(
    napi_env env,
    napi_async_cleanup_hook_handle remove_handle);
```

Unregisters the cleanup hook corresponding to `remove_handle`. This will prevent
the hook from being executed, unless it has already started executing.
This must be called on any `napi_async_cleanup_hook_handle` value retrieved
from [`napi_add_async_cleanup_hook`][].

