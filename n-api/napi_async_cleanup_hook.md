<!-- YAML
added: v14.10.0
-->

Function pointer used with [`napi_add_async_cleanup_hook`][]. It will be called
when the environment is being torn down.

Callback functions must satisfy the following signature:

```c
typedef void (*napi_async_cleanup_hook)(napi_async_cleanup_hook_handle handle,
                                        void* data);
```

* `[in] handle`: The handle that must be passed to
[`napi_remove_async_cleanup_hook`][] after completion of the asynchronous
cleanup.
* `[in] data`: The data that was passed to [`napi_add_async_cleanup_hook`][].

The body of the function should initiate the asynchronous cleanup actions at the
end of which `handle` must be passed in a call to
[`napi_remove_async_cleanup_hook`][].

