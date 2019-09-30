<!-- YAML
added: v10.7.0
-->

> Stability: 1 - Experimental

```C
napi_status napi_create_bigint_uint64(napi_env env,
                                      uint64_t value,
                                      napi_value* result);
```

* `[in] env`: The environment that the API is invoked under.
* `[in] value`: Unsigned integer value to be represented in JavaScript.
* `[out] result`: A `napi_value` representing a JavaScript `BigInt`.

Returns `napi_ok` if the API succeeded.

This API converts the C `uint64_t` type to the JavaScript `BigInt` type.

