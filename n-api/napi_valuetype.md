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
  napi_bigint,
} napi_valuetype;
```

Describes the type of a `napi_value`. This generally corresponds to the types
described in

the ECMAScript Language Specification.
In addition to types in that section, `napi_valuetype` can also represent
`Function`s and `Object`s with external data.

A JavaScript value of type `napi_external` appears in JavaScript as a plain
object such that no properties can be set on it, and no prototype.

