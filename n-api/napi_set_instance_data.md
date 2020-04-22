<!-- YAML
added: v12.8.0
napiVersion: 6
-->

```C
napi_status napi_set_instance_data(napi_env env,
                                   void* data,
                                   napi_finalize finalize_cb,
                                   void* finalize_hint);
```

* `[in] env`: The environment that the N-API call is invoked under.
* `[in] data`: The data item to make available to bindings of this instance.
* `[in] finalize_cb`: The function to call when the environment is being torn
  down. The function receives `data` so that it might free it.
* `[in] finalize_hint`: Optional hint to pass to the finalize callback during
  collection.

Returns `napi_ok` if the API succeeded.

This API associates `data` with the currently running Agent. `data` can later
be retrieved using `napi_get_instance_data()`. Any existing data associated with
the currently running Agent which was set by means of a previous call to
`napi_set_instance_data()` will be overwritten. If a `finalize_cb` was provided
by the previous call, it will not be called.

