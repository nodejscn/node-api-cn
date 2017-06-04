Integral status code indicating the success or failure of a N-API call.
Currently, the following status codes are supported.
```C
typedef enum {
  napi_ok,
  napi_invalid_arg,
  napi_object_expected,
  napi_string_expected,
  napi_name_expected,
  napi_function_expected,
  napi_number_expected,
  napi_boolean_expected,
  napi_array_expected,
  napi_generic_failure,
  napi_pending_exception,
  napi_cancelled,
  napi_status_last
} napi_status;
```
If additional information is required upon an API returning a failed status,
it can be obtained by calling `napi_get_last_error_info`.

