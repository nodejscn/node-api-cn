<!-- YAML
added: v10.6.0
napiVersion: 4
-->

A value to be given to `napi_release_threadsafe_function()` to indicate whether
the thread-safe function is to be closed immediately (`napi_tsfn_abort`) or
merely released (`napi_tsfn_release`) and thus available for subsequent use via
`napi_acquire_threadsafe_function()` and `napi_call_threadsafe_function()`.

```C
typedef enum {
  napi_tsfn_release,
  napi_tsfn_abort
} napi_threadsafe_function_release_mode;
```

