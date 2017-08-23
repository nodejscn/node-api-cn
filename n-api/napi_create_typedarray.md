<!-- YAML
added: v8.0.0
-->
```C
napi_status napi_create_typedarray(napi_env env,
                                   napi_typedarray_type type,
                                   size_t length,
                                   napi_value arraybuffer,
                                   size_t byte_offset,
                                   napi_value* result)
```

- `[in] env`: The environment that the API is invoked under.
- `[in] type`: Scalar datatype of the elements within the TypedArray.
- `[in] length`: Number of elements in the TypedArray.
- `[in] arraybuffer`: ArrayBuffer underlying the typed array.
- `[in] byte_offset`: The byte offset within the ArrayBuffer from which to
start projecting the TypedArray.
- `[out] result`: A `napi_value` representing a JavaScript TypedArray.

Returns `napi_ok` if the API succeeded.

This API creates a JavaScript TypedArray object over an existing ArrayBuffer.
TypedArray objects provide an array-like view over an underlying data buffer
where each element has the same underlying binary scalar datatype.

It's required that (length * size_of_element) + byte_offset should
be <= the size in bytes of the array passed in. If not, a RangeError exception is
raised.

JavaScript TypedArray Objects are described in
[Section 22.2](https://tc39.github.io/ecma262/#sec-typedarray-objects)
of the ECMAScript Language Specification.


