<!-- YAML
added: v8.0.0
-->
```C
NODE_EXTERN napi_status napi_create_reference(napi_env env,
                                              napi_value value,
                                              int initial_refcount,
                                              napi_ref* result);
```

- `[in] env`: The environment that the API is invoked under.
- `[in] value`: `napi_value` representing the Object to which we want
a reference to.
- `[in] initial_refcount`: Initial reference count for the new reference.
- `[out] result`: `napi_ref` pointing to the new reference.

Returns `napi_ok` if the API succeeded.

This API create a new reference with the specified reference count
to the Object passed in.

