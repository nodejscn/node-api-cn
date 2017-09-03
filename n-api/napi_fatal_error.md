<!-- YAML
added: v8.2.0
-->
```C
NAPI_EXTERN NAPI_NO_RETURN void napi_fatal_error(const char* location, const char* message);
```

- `[in] location`: Optional location at which the error occurred.
- `[in] message`: The message associated with the error.

The function call does not return, the process will be terminated.

