
<!-- YAML
added: v10.6.0
napiVersion: 4
-->

```C
NAPI_EXTERN napi_status
napi_release_threadsafe_function(napi_threadsafe_function func,
                                 napi_threadsafe_function_release_mode mode);
```

* `[in] func`: The asynchronous thread-safe JavaScript function whose reference
  count to decrement.
* `[in] mode`: Flag whose value can be either `napi_tsfn_release` to indicate
  that the current thread will make no further calls to the thread-safe
  function, or `napi_tsfn_abort` to indicate that in addition to the current
  thread, no other thread should make any further calls to the thread-safe
  function. If set to `napi_tsfn_abort`, further calls to
  `napi_call_threadsafe_function()` will return `napi_closing`, and no further
  values will be placed in the queue.

A thread should call this API when it stops making use of `func`. Passing `func`
to any thread-safe APIs after having called this API has undefined results, as
`func` may have been destroyed.

This API may be called from any thread which will stop making use of `func`.

