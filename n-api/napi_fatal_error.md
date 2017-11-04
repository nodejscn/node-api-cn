<!-- YAML
added: v8.2.0
-->
```C
NAPI_NO_RETURN void napi_fatal_error(const char* location,
                                                 size_t location_len,
                                                 const char* message,
                                                 size_t message_len);
```

- `[in] location`: Optional location at which the error occurred.
- `[in] location_len`: The length of the location in bytes, or
NAPI_AUTO_LENGTH if it is null-terminated.
- `[in] message`: The message associated with the error.
- `[in] message_len`: The length of the message in bytes, or
NAPI_AUTO_LENGTH if it is
null-terminated.

The function call does not return, the process will be terminated.

