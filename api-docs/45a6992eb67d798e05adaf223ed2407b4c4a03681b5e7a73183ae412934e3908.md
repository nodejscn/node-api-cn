<!-- YAML
added: v8.0.0
napiVersion: 1
-->
```C
napi_status napi_create_string_latin1(napi_env env,
                                      const char* str,
                                      size_t length,
                                      napi_value* result);
```

- `[in] env`: The environment that the API is invoked under.
- `[in] str`: Character buffer representing an ISO-8859-1-encoded string.
- `[in] length`: The length of the string in bytes, or
`NAPI_AUTO_LENGTH` if it is null-terminated.
- `[out] result`: A `napi_value` representing a JavaScript `String`.

Returns `napi_ok` if the API succeeded.

This API creates a JavaScript `String` object from an ISO-8859-1-encoded C
string. The native string is copied.

The JavaScript `String` type is described in
[Section 6.1.4][] of the ECMAScript Language Specification.

