<!-- YAML
added: v8.0.0
-->
```C
napi_status napi_create_symbol(napi_env env,
                               napi_value description,
                               napi_value* result)
```

- `[in] env`: The environment that the API is invoked under.
- `[in] description`: Optional napi_value which refers to a JavaScript
String to be set as the description for the symbol.
- `[out] result`: A `napi_value` representing a JavaScript Symbol.

Returns `napi_ok` if the API succeeded.

This API creates a JavaScript Symbol object from a UTF8-encoded C string

The JavaScript Symbol type is described in
[Section 19.4](https://tc39.github.io/ecma262/#sec-symbol-objects)
of the ECMAScript Language Specification.

