```C
typedef enum {
  // ES6 types (corresponds to typeof)
  napi_undefined,
  napi_null,
  napi_boolean,
  napi_number,
  napi_string,
  napi_symbol,
  napi_object,
  napi_function,
  napi_external,
} napi_valuetype;
```

Describes the type of a `napi_value`. This generally corresponds to the types
described in
[Section 6.1](https://tc39.github.io/ecma262/#sec-ecmascript-language-types) of
the ECMAScript Language Specification.
In addition to types in that section, `napi_valuetype` can also represent
Functions and Objects with external data.

