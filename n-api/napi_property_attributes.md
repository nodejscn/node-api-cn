```C
typedef enum {
  napi_default = 0,
  napi_read_only = 1 << 0,
  napi_dont_enum = 1 << 1,
  napi_dont_delete = 1 << 2,
  napi_static_property = 1 << 10,
} napi_property_attributes;
```

`napi_property_attributes` are flags used to control the behavior of properties
set on a JavaScript object. They roughly correspond to the attributes listed in
[Section 6.1.7.1](https://tc39.github.io/ecma262/#table-2) of the
[ECMAScript Language Specification](https://tc39.github.io/ecma262/). They can
be one or more of the following bitflags:

- `napi_default` - Used to indicate that no explicit attributes are set on the
given property. By default, a property is Writable, Enumerable, and
 Configurable. This is a deviation from the ECMAScript specification,
 where generally the values for a property descriptor attribute default to
 false if they're not provided.
- `napi_read_only` - Used to indicate that a given property is not Writable.
- `napi_dont_enum` - Used to indicate that a given property is not Enumerable.
- `napi_dont_delete` - Used to indicate that a given property is not.
Configurable, as defined in
[Section 6.1.7.1](https://tc39.github.io/ecma262/#table-2) of the
[ECMAScript Language Specification](https://tc39.github.io/ecma262/).
- `napi_static_property` - Used to indicate that the property will be defined as
a static property on a class as opposed to an instance property, which is the
default. This is used only by [`napi_define_class`][]. It is ignored by
`napi_define_properties`.

