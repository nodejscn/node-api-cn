<!-- YAML
added: v8.0.0
napiVersion: 1
-->

```C
napi_status napi_get_and_clear_last_exception(napi_env env,
                                              napi_value* result);
```

* `[in] env`: The environment that the API is invoked under.
* `[out] result`: The exception if one is pending, NULL otherwise.

Returns `napi_ok` if the API succeeded.

This API can be called even if there is a pending JavaScript exception.

