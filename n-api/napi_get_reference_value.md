<!-- YAML
added: v8.0.0
-->
```C
NODE_EXTERN napi_status napi_get_reference_value(napi_env env,
                                                 napi_ref ref,
                                                 napi_value* result);
```

the `napi_value passed` in or out of these methods is a handle to the
object to which the reference is related.
- `[in] env`: The environment that the API is invoked under.
- `[in] ref`: `napi_ref` for which we requesting the corresponding Object.
- `[out] result`: The `napi_value` for the Object referenced by the
`napi_ref`.

Returns `napi_ok` if the API succeeded.

If still valid, this API returns the `napi_value` representing the
JavaScript Object associated with the `napi_ref`. Otherise, result
will be NULL.

