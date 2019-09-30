<!-- YAML
added: v8.0.0
napiVersion: 1
-->

```C
NAPI_EXTERN napi_status napi_is_error(napi_env env,
                                      napi_value value,
                                      bool* result);
```

* `[in] env`: The environment that the API is invoked under.
* `[in] value`: The `napi_value` to be checked.
* `[out] result`: Boolean value that is set to true if `napi_value` represents
an error, false otherwise.

Returns `napi_ok` if the API succeeded.

This API queries a `napi_value` to check if it represents an error object.

