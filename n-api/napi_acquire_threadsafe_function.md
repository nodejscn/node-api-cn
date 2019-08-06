
<!-- YAML
added: v10.6.0
napiVersion: 4
-->
```C
NAPI_EXTERN napi_status
napi_acquire_threadsafe_function(napi_threadsafe_function func);
```

- `[in] func`: The asynchronous thread-safe JavaScript function to start making
use of.

A thread should call this API before passing `func` to any other thread-safe
function APIs to indicate that it will be making use of `func`. This prevents
`func` from being destroyed when all other threads have stopped making use of
it.

This API may be called from any thread which will start making use of `func`.

