
> Stability: 2 - Stable

<!-- YAML
added: v10.6.0
-->
```C
NAPI_EXTERN napi_status
napi_call_threadsafe_function(napi_threadsafe_function func,
                              void* data,
                              napi_threadsafe_function_call_mode is_blocking);
```

- `[in] func`: The asynchronous thread-safe JavaScript function to invoke.
- `[in] data`: Data to send into JavaScript via the callback `call_js_cb`
provided during the creation of the thread-safe JavaScript function.
- `[in] is_blocking`: Flag whose value can be either `napi_tsfn_blocking` to
indicate that the call should block if the queue is full or
`napi_tsfn_nonblocking` to indicate that the call should return immediately with
a status of `napi_queue_full` whenever the queue is full.

This API will return `napi_closing` if `napi_release_threadsafe_function()` was
called with `abort` set to `napi_tsfn_abort` from any thread. The value is only
added to the queue if the API returns `napi_ok`.

This API may be called from any thread which makes use of `func`.

