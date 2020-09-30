<!-- YAML
added: v8.0.0
napiVersion: 1
-->

```c
napi_status napi_get_value_string_latin1(napi_env env,
                                         napi_value value,
                                         char* buf,
                                         size_t bufsize,
                                         size_t* result)
```

* `[in] env`: The environment that the API is invoked under.
* `[in] value`: `napi_value` representing JavaScript string.
* `[in] buf`: Buffer to write the ISO-8859-1-encoded string into. If `NULL` is
  passed in, the length of the string in bytes and excluding the null terminator
  is returned in `result`.
* `[in] bufsize`: Size of the destination buffer. When this value is
  insufficient, the returned string is truncated and null-terminated.
* `[out] result`: Number of bytes copied into the buffer, excluding the null
  terminator.

Returns `napi_ok` if the API succeeded. If a non-`String` `napi_value`
is passed in it returns `napi_string_expected`.

This API returns the ISO-8859-1-encoded string corresponding the value passed
in.

