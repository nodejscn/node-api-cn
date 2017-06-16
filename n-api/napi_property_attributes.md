```C
typedef enum {
  napi_default = 0,
  napi_writable = 1 << 0,
  napi_enumerable = 1 << 1,
  napi_configurable = 1 << 2,

  // Used with napi_define_class to distinguish static properties
  // from instance properties. Ignored by napi_define_properties.
  napi_static = 1 << 10,
} napi_property_attributes;
```

`napi_property_attributes` are flags used to control the behavior of properties
set on a JavaScript object. Other than `napi_static` they correspond to the
attributes listed in [Section 6.1.7.1](https://tc39.github.io/ecma262/#table-2)
of the [ECMAScript Language Specification](https://tc39.github.io/ecma262/).
They can be one or more of the following bitflags:

- `napi_default` - Used to indicate that no explicit attributes are set on the
given property. By default, a property is read only, not enumerable and not
configurable.
- `napi_writable`  - Used to indicate that a given property is writable.
- `napi_enumerable` - Used to indicate that a given property is enumerable.
- `napi_configurable` - Used to indicate that a given property is
configurable, as defined in
[Section 6.1.7.1](https://tc39.github.io/ecma262/#table-2) of the
[ECMAScript Language Specification](https://tc39.github.io/ecma262/).
- `napi_static` - Used to indicate that the property will be defined as
a static property on a class as opposed to an instance property, which is the
default. This is used only by [`napi_define_class`][]. It is ignored by
`napi_define_properties`.

