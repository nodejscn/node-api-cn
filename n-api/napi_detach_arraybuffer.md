<!-- YAML
added:
 - v13.0.0
 - v12.16.0
-->

> Stability: 1 - Experimental

```c
napi_status napi_detach_arraybuffer(napi_env env,
                                    napi_value arraybuffer)
```

* `[in] env`: The environment that the API is invoked under.
* `[in] arraybuffer`: The JavaScript `ArrayBuffer` to be detached.

Returns `napi_ok` if the API succeeded. If a non-detachable `ArrayBuffer` is
passed in it returns `napi_detachable_arraybuffer_expected`.

Generally, an `ArrayBuffer` is non-detachable if it has been detached before.
The engine may impose additional conditions on whether an `ArrayBuffer` is
detachable. For example, V8 requires that the `ArrayBuffer` be external,
that is, created with [`napi_create_external_arraybuffer`][].

This API represents the invocation of the `ArrayBuffer` detach operation as
defined in [Section 24.1.1.3][] of the ECMAScript Language Specification.

