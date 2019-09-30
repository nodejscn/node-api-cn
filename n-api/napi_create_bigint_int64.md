<!-- YAML
added: v10.7.0
-->

> Stability: 1 - Experimental

```C
napi_status napi_create_bigint_int64(napi_env env,
                                     int64_t value,
                                     napi_value* result);
```

* `[in] env`: The environment that the API is invoked under.
* `[in] value`: Integer value to be represented in JavaScript.
* `[out] result`: A `napi_value` representing a JavaScript `BigInt`.

Returns `napi_ok` if the API succeeded.

This API converts the C `int64_t` type to the JavaScript `BigInt` type.

