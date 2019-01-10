<!-- YAML
added: v8.0.0
napiVersion: 1
-->
```C
napi_status napi_get_value_int64(napi_env env,
                                 napi_value value,
                                 int64_t* result)
```

- `[in] env`: The environment that the API is invoked under.
- `[in] value`: `napi_value` representing JavaScript `Number`.
- `[out] result`: C `int64` primitive equivalent of the given JavaScript
  `Number`.

Returns `napi_ok` if the API succeeded. If a non-number `napi_value`
is passed in it returns `napi_number_expected`.

This API returns the C `int64` primitive equivalent of the given JavaScript
`Number`.

`Number` values outside the range of

-(2^53 - 1) -

(2^53 - 1) will lose precision.

Non-finite number values (`NaN`, `+Infinity`, or `-Infinity`) set the
result to zero.

