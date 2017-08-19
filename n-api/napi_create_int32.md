<!-- YAML
added: v8.4.0
-->
```C
napi_status napi_create_int32(napi_env env, int32_t value, napi_value* result)
```

- `[in] env`: The environment that the API is invoked under.
- `[in] value`: Integer value to be represented in JavaScript.
- `[out] result`: A `napi_value` representing a JavaScript Number.

Returns `napi_ok` if the API succeeded.

This API is used to convert from the C `int32_t` type to the JavaScript
Number type.

The JavaScript Number type is described in
[Section 6.1.6](https://tc39.github.io/ecma262/#sec-ecmascript-language-types-number-type)
of the ECMAScript Language Specification.

