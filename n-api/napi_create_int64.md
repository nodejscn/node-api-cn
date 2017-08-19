<!-- YAML
added: v8.4.0
-->
```C
napi_status napi_create_int64(napi_env env, int64_t value, napi_value* result)
```

- `[in] env`: The environment that the API is invoked under.
- `[in] value`: Integer value to be represented in JavaScript.
- `[out] result`: A `napi_value` representing a JavaScript Number.

Returns `napi_ok` if the API succeeded.

This API is used to convert from the C `int64_t` type to the JavaScript
Number type.

The JavaScript Number type is described in
[Section 6.1.6](https://tc39.github.io/ecma262/#sec-ecmascript-language-types-number-type)
of the ECMAScript Language Specification. Note the complete range of `int64_t`
cannot be represented with full precision in JavaScript. Integer values
outside the range of
[`Number.MIN_SAFE_INTEGER`](https://tc39.github.io/ecma262/#sec-number.min_safe_integer)
-(2^53 - 1) -
[`Number.MAX_SAFE_INTEGER`](https://tc39.github.io/ecma262/#sec-number.max_safe_integer)
(2^53 - 1) will lose precision.

