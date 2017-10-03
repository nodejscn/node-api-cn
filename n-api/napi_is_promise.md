<!-- YAML
added: v8.5.0
-->
```C
napi_status napi_is_promise(napi_env env,
                            napi_value promise,
                            bool* is_promise);
```

- `[in] env`: The environment that the API is invoked under.
- `[in] promise`: The promise to examine
- `[out] is_promise`: Flag indicating whether `promise` is a native promise
object - that is, a promise object created by the underlying engine.

