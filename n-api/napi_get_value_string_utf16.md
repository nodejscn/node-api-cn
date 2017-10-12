<!-- YAML
added: v8.0.0
-->
```C
napi_status napi_get_value_string_utf16(napi_env env,
                                        napi_value value,
                                        char16_t* buf,
                                        size_t bufsize,
                                        size_t* result)
```

- `[in] env`: The environment that the API is invoked under.
- `[in] value`: `napi_value` representing JavaScript string.
- `[in] buf`: Buffer to write the UTF16-LE-encoded string into. If NULL is
passed in, the length of the string (in 2-byte code units) is returned.
- `[in] bufsize`: Size of the destination buffer. When this value is
insufficient, the returned string will be truncated.
- `[out] result`: Number of 2-byte code units copied into the buffer, excluding the null
terminator.

Returns `napi_ok` if the API succeeded. If a non-String `napi_value`
is passed in it returns `napi_string_expected`.

This API returns the UTF16-encoded string corresponding the value passed in.

