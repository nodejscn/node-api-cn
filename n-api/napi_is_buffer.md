<!-- YAML
added: v8.0.0
-->
```C
napi_status napi_is_buffer(napi_env env, napi_value value, bool* result)
```

- `[in] env`: The environment that the API is invoked under.
- `[in] value`: The JavaScript value to check.
- `[out] result`: Whether the given `napi_value` represents a `node::Buffer`
object.

Returns `napi_ok` if the API succeeded.

This API checks if the Object passsed in is a buffer.

