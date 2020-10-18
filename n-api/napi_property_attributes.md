<!-- YAML
changes:
 - version: v14.12.0
   pr-url: https://github.com/nodejs/node/pull/35214
   description: added `napi_default_method` and `napi_default_property`.
-->

```c
typedef enum {
  napi_default = 0,
  napi_writable = 1 << 0,
  napi_enumerable = 1 << 1,
  napi_configurable = 1 << 2,

  // Used with napi_define_class to distinguish static properties
  // from instance properties. Ignored by napi_define_properties.
  napi_static = 1 << 10,

  // Default for class methods.
  napi_default_method = napi_writable | napi_configurable,

  // Default for object properties, like in JS obj[prop].
  napi_default_property = napi_writable |
                          napi_enumerable |
                          napi_configurable,
} napi_property_attributes;
```

`napi_property_attributes` are flags used to control the behavior of properties
set on a JavaScript object. Other than `napi_static` they correspond to the
attributes listed in [Section 6.1.7.1][]
of the [ECMAScript Language Specification][].
They can be one or more of the following bitflags:

* `napi_default`: No explicit attributes are set on the property. By default, a
  property is read only, not enumerable and not configurable.
* `napi_writable`: The property is writable.
* `napi_enumerable`: The property is enumerable.
* `napi_configurable`: The property is configurable as defined in
  [Section 6.1.7.1][] of the [ECMAScript Language Specification][].
* `napi_static`: The property will be defined as a static property on a class as
  opposed to an instance property, which is the default. This is used only by
  [`napi_define_class`][]. It is ignored by `napi_define_properties`.
* `napi_default_method`: Like a method in a JS class, the property is
  configurable and writeable, but not enumerable.
* `napi_default_property`: Like a property set via assignment in JavaScript, the
  property is writable, enumerable, and configurable.

