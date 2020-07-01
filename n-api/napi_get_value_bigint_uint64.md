<!-- YAML
added: v10.7.0
napiVersion: 6
-->

```c
napi_status napi_get_value_bigint_uint64(napi_env env,
                                        napi_value value,
                                        uint64_t* result,
                                        bool* lossless);
```

* `[in] env`: The environment that the API is invoked under.
* `[in] value`: `napi_value` representing JavaScript `BigInt`.
* `[out] result`: C `uint64_t` primitive equivalent of the given JavaScript
  `BigInt`.
* `[out] lossless`: Indicates whether the `BigInt` value was converted
  losslessly.

Returns `napi_ok` if the API succeeded. If a non-`BigInt` is passed in it
returns `napi_bigint_expected`.

This API returns the C `uint64_t` primitive equivalent of the given JavaScript
`BigInt`. If needed it will truncate the value, setting `lossless` to `false`.

