<!-- YAML
added: v8.0.0
napiVersion: 1
-->

```c
napi_status napi_is_array(napi_env env, napi_value value, bool* result)
```

* `[in] env`: The environment that the API is invoked under.
* `[in] value`: The JavaScript value to check.
* `[out] result`: Whether the given object is an array.

Returns `napi_ok` if the API succeeded.

This API represents invoking the `IsArray` operation on the object
as defined in [Section 7.2.2][] of the ECMAScript Language Specification.

