<!-- YAML
added: v8.0.0
-->
```C
napi_status napi_create_string_utf16(napi_env env,
                                     const char16_t* str,
                                     size_t length,
                                     napi_value* result)
```

- `[in] env`: The environment that the API is invoked under.
- `[in] str`: Character buffer representing a UTF16-LE-encoded string.
- `[in] length`: The length of the string in two-byte code units, or -1 if
it is null-terminated.
- `[out] result`: A `napi_value` representing a JavaScript String.

Returns `napi_ok` if the API succeeded.

This API creates a JavaScript String object from a UTF16-LE-encoded C string

The JavaScript String type is described in
[Section 6.1.4](https://tc39.github.io/ecma262/#sec-ecmascript-language-types-string-type)
of the ECMAScript Language Specification.

