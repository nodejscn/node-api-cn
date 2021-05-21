
<!-- YAML
added:
  - v15.9.0
  - v12.22.0
-->

> Stability: 1 - Experimental

```c
NAPI_EXTERN napi_status
node_api_get_module_file_name(napi_env env, const char** result);

```

* `[in] env`: The environment that the API is invoked under.
* `[out] result`: A URL containing the absolute path of the
  location from which the add-on was loaded. For a file on the local
  file system it will start with `file://`. The string is null-terminated and
  owned by `env` and must thus not be modified or freed.

`result` may be an empty string if the add-on loading process fails to establish
the add-on's file name during loading.


























































































































