<!-- YAML
added: v8.0.0
napiVersion: 1
-->

```c
napi_status napi_create_array(napi_env env, napi_value* result)
```

* `[in] env`: The environment that the Node-API call is invoked under.
* `[out] result`: A `napi_value` representing a JavaScript `Array`.

Returns `napi_ok` if the API succeeded.

This API returns a Node-API value corresponding to a JavaScript `Array` type.
JavaScript arrays are described in
[Section 22.1][] of the ECMAScript Language Specification.

