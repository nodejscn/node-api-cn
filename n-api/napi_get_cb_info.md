<!-- YAML
added: v8.0.0
-->
```C
napi_status napi_get_cb_info(napi_env env,
                             napi_callback_info cbinfo,
                             size_t* argc,
                             napi_value* argv,
                             napi_value* thisArg,
                             void** data)
```

- `[in] env`: The environment that the API is invoked under.
- `[in] cbinfo`: The callback info passed into the callback function.
- `[in-out] argc`: Specifies the size of the provided `argv` array
and receives the actual count of arguments.
- `[out] argv`: Buffer to which the `napi_value` representing the
arguments are copied. If there are more arguments than the provided
count, only the requested number of arguments are copied. If there are fewer
arguments provided than claimed, the rest of `argv` is filled with `napi_value`
values that represent `undefined`.
- `[out] this`: Receives the JavaScript `this` argument for the call.
- `[out] data`: Receives the data pointer for the callback.

Returns `napi_ok` if the API succeeded.

This method is used within a callback function to retrieve details about the
call like the arguments and the `this` pointer from a given callback info.

