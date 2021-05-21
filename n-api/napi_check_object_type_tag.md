<!-- YAML
added:
  - v14.8.0
  - v12.19.0
napiVersion: 8
-->

```c
napi_status napi_check_object_type_tag(napi_env env,
                                       napi_value js_object,
                                       const napi_type_tag* type_tag,
                                       bool* result);
```

* `[in] env`: The environment that the API is invoked under.
* `[in] js_object`: The JavaScript object whose type tag to examine.
* `[in] type_tag`: The tag with which to compare any tag found on the object.
* `[out] result`: Whether the type tag given matched the type tag on the
  object. `false` is also returned if no type tag was found on the object.

Returns `napi_ok` if the API succeeded.

Compares the pointer given as `type_tag` with any that can be found on
`js_object`. If no tag is found on `js_object` or, if a tag is found but it does
not match `type_tag`, then `result` is set to `false`. If a tag is found and it
matches `type_tag`, then `result` is set to `true`.

