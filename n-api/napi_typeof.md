<!-- YAML
added: v8.0.0
-->
```C
napi_status napi_typeof(napi_env env, napi_value value, napi_valuetype* result)
```

- `[in] env`: The environment that the API is invoked under.
- `[in] value`: The JavaScript value whose type to query.
- `[out] result`: The type of the JavaScript value.

Returns `napi_ok` if the API succeeded.
- `napi_invalid_arg` if the type of `value` is not a known ECMAScript type and
 `value` is not an External value.

This API represents behavior similar to invoking the `typeof` Operator on
the object as defined in [Section 12.5.5][] of the ECMAScript Language
Specification. However, it has support for detecting an External value.
If `value` has a type that is invalid, an error is returned.

