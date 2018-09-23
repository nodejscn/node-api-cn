<!-- YAML
added: v9.6.0
napiVersion: 3
-->
```C
NAPI_EXTERN napi_status napi_open_callback_scope(napi_env env,
                                                 napi_value resource_object,
                                                 napi_async_context context,
                                                 napi_callback_scope* result)
```
- `[in] env`: The environment that the API is invoked under.
- `[in] resource_object`: An optional object associated with the async work
  that will be passed to possible `async_hooks` [`init` hooks][].
- `[in] context`: Context for the async operation that is
invoking the callback. This should be a value previously obtained
from [`napi_async_init`][].
- `[out] result`: The newly created scope.

There are cases (for example, resolving promises) where it is
necessary to have the equivalent of the scope associated with a callback
in place when making certain N-API calls. If there is no other script on
the stack the [`napi_open_callback_scope`][] and
[`napi_close_callback_scope`][] functions can be used to open/close
the required scope.

