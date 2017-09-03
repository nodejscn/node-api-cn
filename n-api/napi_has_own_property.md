<!-- YAML
added: v8.2.0
-->
```C
napi_status napi_has_own_property(napi_env env,
                                  napi_value object,
                                  napi_value key,
                                  bool* result);
```

- `[in] env`: The environment that the N-API call is invoked under.
- `[in] object`: The object to query.
- `[in] key`: The name of the own property whose existence to check.
- `[out] result`: Whether the own property exists on the object or not.

Returns `napi_ok` if the API succeeded.

This API checks if the Object passed in has the named own property. `key` must
be a string or a Symbol, or an error will be thrown. N-API will not perform any
conversion between data types.


