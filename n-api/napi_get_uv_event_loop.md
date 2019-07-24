<!-- YAML
added:
  - v8.10.0
  - v9.3.0
napiVersion: 2
-->
```C
NAPI_EXTERN napi_status napi_get_uv_event_loop(napi_env env,
                                               uv_loop_t** loop);
```

- `[in] env`: The environment that the API is invoked under.
- `[out] loop`: The current libuv loop instance.

<!-- it's very convenient to have all the anchors indexed -->
<!--lint disable no-unused-definitions remark-lint-->
