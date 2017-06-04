<!-- YAML
added: v8.0.0
-->
```C
napi_status napi_get_property_names(napi_env env,
                                    napi_value object,
                                    napi_value* result);
```

- `[in] env`: The environment that the N-API call is invoked under.
- `[in] object`: The object from which to retrieve the properties.
- `[out] result`: A `napi_value` representing an array of JavaScript values
that represent the property names of the object. The API can be used to
iterate over `result` using [`napi_get_array_length`][]
and [`napi_get_element`][].

Returns `napi_ok` if the API succeeded.

This API returns the array of propertys for the Object passed in

