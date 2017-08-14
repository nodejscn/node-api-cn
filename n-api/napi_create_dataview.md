<!-- YAML
added: v8.3.0
-->

```C
napi_status napi_create_dataview(napi_env env,
                                 size_t byte_length,
                                 napi_value arraybuffer,
                                 size_t byte_offset,
                                 napi_value* result)

```

- `[in] env`: The environment that the API is invoked under.
- `[in] length`: Number of elements in the DataView.
- `[in] arraybuffer`: ArrayBuffer underlying the DataView.
- `[in] byte_offset`: The byte offset within the ArrayBuffer from which to
  start projecting the DataView.
- `[out] result`: A `napi_value` representing a JavaScript DataView.

Returns `napi_ok` if the API succeeded.

This API creates a JavaScript DataView object over an existing ArrayBuffer.
DataView objects provide an array-like view over an underlying data buffer,
but one which allows items of different size and type in the ArrayBuffer.

It is required that `byte_length + byte_offset` is less than or equal to the
size in bytes of the array passed in. If not, a RangeError exception is raised.

JavaScript DataView Objects are described in
[Section 24.3][] of the ECMAScript Language Specification.

