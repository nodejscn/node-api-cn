Function pointer type for user-provided native functions which are to be
exposed to JavaScript via N-API. Callback functions should satisfy the
following signature:
```C
typedef napi_value (*napi_callback)(napi_env, napi_callback_info);
```

