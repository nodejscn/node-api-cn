All of the N-API functions share the same error handling pattern. The
return type of all API functions is `napi_status`.

The return value will be `napi_ok` if the request was successful and
no uncaught JavaScript exception was thrown. If an error occurred AND
an exception was thrown, the `napi_status` value for the error
will be returned. If an exception was thrown, and no error occurred,
`napi_pending_exception` will be returned.

In cases where a return value other than `napi_ok` or
`napi_pending_exception` is returned, [`napi_is_exception_pending`][]
must be called to check if an exception is pending.
See the section on exceptions for more details.

The full set of possible napi_status values is defined
in `napi_api_types.h`.

The `napi_status` return value provides a VM-independent representation of
the error which occurred. In some cases it is useful to be able to get
more detailed information, including a string representing the error as well as
VM (engine)-specific information.

In order to retrieve this information [`napi_get_last_error_info`][]
is provided which returns a `napi_extended_error_info` structure.
The format of the `napi_extended_error_info` structure is as follows:

```C
typedef struct napi_extended_error_info {
  const char* error_message;
  void* engine_reserved;
  uint32_t engine_error_code;
  napi_status error_code;
};
```
- `error_message`: Textual representation of the error that occurred.
- `engine_reserved`: Opaque handle reserved for engine use only.
- `engine_error_code`: VM specific error code.
- `error_code`: n-api status code for the last error.

[`napi_get_last_error_info`][] returns the information for the last
N-API call that was made.

*Note*: Do not rely on the content or format of any of the extended
information as it is not subject to SemVer and may change at any time.
It is intended only for logging purposes.

