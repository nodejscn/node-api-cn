<!-- YAML
added: v8.4.0
-->
```C
napi_status napi_create_uint32(napi_env env, uint32_t value, napi_value* result)
```

- `[in] env`: The environment that the API is invoked under.
- `[in] value`: Unsigned integer value to be represented in JavaScript.
- `[out] result`: A `napi_value` representing a JavaScript Number.

Returns `napi_ok` if the API succeeded.

This API is used to convert from the C `uint32_t` type to the JavaScript
Number type.

The JavaScript Number type is described in
[Section 6.1.6](https://tc39.github.io/ecma262/#sec-ecmascript-language-types-number-type)
of the ECMAScript Language Specification.

