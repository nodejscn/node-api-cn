<!-- YAML
added: v8.0.0
-->
```C
napi_status napi_create_object(napi_env env, napi_value* result)
```

- `[in] env`: The environment that the API is invoked under.
- `[out] result`: A `napi_value` representing a JavaScript Object.

Returns `napi_ok` if the API succeeded.

This API allocates a default JavaScript Object.
It is the equivalent of doing `new Object()` in JavaScript.

The JavaScript Object type is described in
[Section 6.1.7](https://tc39.github.io/ecma262/#sec-object-type) of the
ECMAScript Language Specification.

