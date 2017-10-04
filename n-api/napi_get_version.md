<!-- YAML
added: v8.0.0
-->
```C
napi_status napi_get_version(napi_env env,
                             uint32_t* result);
```

- `[in] env`: The environment that the API is invoked under.
- `[out] result`: The highest version of N-API supported.

Returns `napi_ok` if the API succeeded.

This API returns the highest N-API version supported by the
Node.js runtime.  N-API is planned to be additive such that
newer releases of Node.js may support additional API functions.
In order to allow an addon to use a newer function when running with
versions of Node.js that support it, while providing
fallback behavior when running with Node.js versions that don't
support it:

* Call `napi_get_version()` to determine if the API is available.
* If available, dynamically load a pointer to the function using `uv_dlsym()`.
* Use the dynamically loaded pointer to invoke the function.
* If the function is not available, provide an alternate implementation
  that does not use the function.

