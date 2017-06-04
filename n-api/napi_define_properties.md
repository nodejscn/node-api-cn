<!-- YAML
added: v8.0.0
-->
```C
napi_status napi_define_properties(napi_env env,
                                   napi_value object,
                                   size_t property_count,
                                   const napi_property_descriptor* properties);
```

- `[in] env`: The environment that the N-API call is invoked under.
- `[in] object`: The object from which to retrieve the properties.
- `[in] property_count`: The number of elements in the `properties` array.
- `[in] properties`: The array of property descriptors.

Returns `napi_ok` if the API succeeded.

This method allows the efficient definition of multiple properties on a given
object. The properties are defined using property descriptors (See
[`napi_property_descriptor`][]). Given an array of such property descriptors, this
API will set the properties on the object one at a time, as defined by
DefineOwnProperty (described in [Section 9.1.6][] of the ECMA262 specification).

