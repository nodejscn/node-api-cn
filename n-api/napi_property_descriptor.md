```C
typedef struct {
  const char* utf8name;

  napi_callback method;
  napi_callback getter;
  napi_callback setter;
  napi_value value;

  napi_property_attributes attributes;
  void* data;
} napi_property_descriptor;
```

- `utf8name`: String describing the key for the property, encoded as UTF8.
- `value`: The value that's retrieved by a get access of the property if the
 property is a data property. If this is passed in, set `getter`, `setter`,
 `method` and `data` to `NULL` (since these members won't be used).
- `getter`: A function to call when a get access of the property is performed.
If this is passed in, set `value` and `method` to `NULL` (since these members
won't be used). The given function is called implicitly by the runtime when the
property is accessed from JavaScript code (or if a get on the property is
performed using a N-API call).
- `setter`: A function to call when a set access of the property is performed.
If this is passed in, set `value` and `method` to `NULL` (since these members
won't be used). The given function is called implicitly by the runtime when the
property is set from JavaScript code (or if a set on the property is
performed using a N-API call).
- `method`: Set this to make the property descriptor object's `value`
property to be a JavaScript function represented by `method`. If this is
passed in, set `value`, `getter` and `setter` to `NULL` (since these members
won't be used).
- `data`: The callback data passed into `method`, `getter` and `setter` if
this function is invoked.
- `attributes`: The attributes associated with the particular property.
See [`napi_property_attributes`](#napi_property_attributes).

