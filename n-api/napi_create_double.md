<!-- YAML
added: v8.4.0
napiVersion: 1
-->

```c
napi_status napi_create_double(napi_env env, double value, napi_value* result)
```

* `[in] env`: The environment that the API is invoked under.
* `[in] value`: Double-precision value to be represented in JavaScript.
* `[out] result`: A `napi_value` representing a JavaScript `Number`.

Returns `napi_ok` if the API succeeded.

This API is used to convert from the C `double` type to the JavaScript
`Number` type.

The JavaScript `Number` type is described in
[Section 6.1.6][] of the ECMAScript Language Specification.

