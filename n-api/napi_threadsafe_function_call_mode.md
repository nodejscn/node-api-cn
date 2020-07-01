<!-- YAML
added: v10.6.0
napiVersion: 4
-->

A value to be given to `napi_call_threadsafe_function()` to indicate whether
the call should block whenever the queue associated with the thread-safe
function is full.

```c
typedef enum {
  napi_tsfn_nonblocking,
  napi_tsfn_blocking
} napi_threadsafe_function_call_mode;
```

