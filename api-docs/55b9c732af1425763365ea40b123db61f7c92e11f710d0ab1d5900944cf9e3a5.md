```C
typedef struct {
  const char* error_message;
  void* engine_reserved;
  uint32_t engine_error_code;
  napi_status error_code;
} napi_extended_error_info;
```

- `error_message`: UTF8-encoded string containing a VM-neutral description of
  the error.
- `engine_reserved`: Reserved for VM-specific error details. This is currently
  not implemented for any VM.
- `engine_error_code`: VM-specific error code. This is currently
  not implemented for any VM.
- `error_code`: The N-API status code that originated with the last error.

See the [Error Handling][] section for additional information.

