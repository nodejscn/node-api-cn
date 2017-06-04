```C
typedef enum {
  napi_int8_array,
  napi_uint8_array,
  napi_uint8_clamped_array,
  napi_int16_array,
  napi_uint16_array,
  napi_int32_array,
  napi_uint32_array,
  napi_float32_array,
  napi_float64_array,
} napi_typedarray_type;
```

This represents the underlying binary scalar datatype of the TypedArray.
Elements of this enum correspond to
[Section 22.2](https://tc39.github.io/ecma262/#sec-typedarray-objects)
of the [ECMAScript Language Specification][].

