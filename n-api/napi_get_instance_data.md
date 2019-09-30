<!-- YAML
added: v12.8.0
-->

```C
napi_status napi_get_instance_data(napi_env env,
                                   void** data);
```

* `[in] env`: The environment that the N-API call is invoked under.
* `[out] data`: The data item that was previously associated with the currently
running Agent by a call to `napi_set_instance_data()`.

Returns `napi_ok` if the API succeeded.

This API retrieves data that was previously associated with the currently
running Agent via `napi_set_instance_data()`. If no data is set, the call will
succeed and `data` will be set to `NULL`.

