<!-- YAML
added:
 - v13.7.0
 - v10.20.0
napiVersion: 6
-->

```c
napi_get_all_property_names(napi_env env,
                            napi_value object,
                            napi_key_collection_mode key_mode,
                            napi_key_filter key_filter,
                            napi_key_conversion key_conversion,
                            napi_value* result);
```

* `[in] env`: The environment that the N-API call is invoked under.
* `[in] object`: The object from which to retrieve the properties.
* `[in] key_mode`: Whether to retrieve prototype properties as well.
* `[in] key_filter`: Which properties to retrieve
(enumerable/readable/writable).
* `[in] key_conversion`: Whether to convert numbered property keys to strings.
* `[out] result`: A `napi_value` representing an array of JavaScript values
that represent the property names of the object. [`napi_get_array_length`][] and
[`napi_get_element`][] can be used to iterate over `result`.

Returns `napi_ok` if the API succeeded.

This API returns an array containing the names of the available properties
of this object.

