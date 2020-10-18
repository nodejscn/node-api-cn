<!-- YAML
added:
  - v9.3.0
  - v8.10.0
napiVersion: 2
-->

```c
NAPI_EXTERN napi_status napi_get_uv_event_loop(napi_env env,
                                               struct uv_loop_s** loop);
```

* `[in] env`: The environment that the API is invoked under.
* `[out] loop`: The current libuv loop instance.

