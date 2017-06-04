<!-- YAML
added: v8.0.0
-->
```C
napi_status napi_get_value_int32(napi_env env,
                                 napi_value value,
                                 int32_t* result)
```

- `[in] env`: The environment that the API is invoked under.
- `[in] value`: `napi_value` representing JavaScript Number.
- `[out] result`: C int32 primitive equivalent of the given JavaScript Number.

Returns `napi_ok` if the API succeeded. If a non-number `napi_value`
is passed in `napi_number_expected .

This API returns the C int32 primitive equivalent
of the given JavaScript Number. If the number exceeds the range of the
32 bit integer, then the result is truncated to the equivalent of the
bottom 32 bits. This can result in a large positive number becoming
a negative number if the the value is > 2^31 -1.

