<!-- YAML
added:
  - v14.8.0
  - v12.19.0
changes:
  - version:
    - v14.10.0
    - v12.19.0
    pr-url: https://github.com/nodejs/node/pull/34819
    description: Removed `env` parameter.
-->

```c
NAPI_EXTERN napi_status napi_remove_async_cleanup_hook(
    napi_async_cleanup_hook_handle remove_handle);
```

* `[in] remove_handle`: The handle to an asynchronous cleanup hook that was
  created with [`napi_add_async_cleanup_hook`][].

Unregisters the cleanup hook corresponding to `remove_handle`. This will prevent
the hook from being executed, unless it has already started executing.
This must be called on any `napi_async_cleanup_hook_handle` value obtained
from [`napi_add_async_cleanup_hook`][].

