<!-- YAML
added: v12.16.0
-->

> Stability: 1 - Experimental

```C
napi_status napi_is_detached_arraybuffer(napi_env env,
                                         napi_value arraybuffer,
                                         bool* result)
```

* `[in] env`: The environment that the API is invoked under.
* `[in] arraybuffer`: The JavaScript `ArrayBuffer` to be checked.
* `[out] result`: Whether the `arraybuffer` is detached.

Returns `napi_ok` if the API succeeded.

The `ArrayBuffer` is considered detached if its internal data is `null`.

This API represents the invocation of the `ArrayBuffer` `IsDetachedBuffer`
operation as defined in [Section 24.1.1.2][] of the ECMAScript Language
Specification.

