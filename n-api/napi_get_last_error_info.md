<!-- YAML
added: v8.0.0
-->
```C
NAPI_EXTERN napi_status
napi_get_last_error_info(napi_env env,
                         const napi_extended_error_info** result);
```
- `[in] env`: The environment that the API is invoked under.
- `[out] result`: The `napi_extended_error_info` structure with more
information about the error.

Returns `napi_ok` if the API succeeded.

This API retrieves a `napi_extended_error_info` structure with information
about the last error that occurred.

*Note*: The content of the `napi_extended_error_info` returned is only
valid up until an n-api function is called on the same `env`.

*Note*: Do not rely on the content or format of any of the extended
information as it is not subject to SemVer and may change at any time.
It is intended only for logging purposes.


