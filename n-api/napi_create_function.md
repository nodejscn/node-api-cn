<!-- YAML
added: v8.0.0
-->
```C
napi_status napi_create_function(napi_env env,
                                 const char* utf8name,
                                 napi_callback cb,
                                 void* data,
                                 napi_value* result)
```

- `[in] env`: The environment that the API is invoked under.
- `[in] utf8name`: A string representing the name of the function encoded as
UTF8.
- `[in] cb`: A function pointer to the native function to be invoked when the
created function is invoked from JavaScript.
- `[in] data`: Optional arbitrary context data to be passed into the native
function when it is invoked.
- `[out] result`: A `napi_value` representing a JavaScript function.

Returns `napi_ok` if the API succeeded.

This API returns an N-API value corresponding to a JavaScript Function object.
It's used to wrap native functions so that they can be invoked from JavaScript.

JavaScript Functions are described in
[Section 19.2](https://tc39.github.io/ecma262/#sec-function-objects)
of the ECMAScript Language Specification.

