<!-- YAML
added: v14.8.0
-->

> Stability: 1 - Experimental

```c
napi_status napi_type_tag_object(napi_env env,
                                 napi_value js_object,
                                 const napi_type_tag* type_tag);
```

* `[in] env`: The environment that the API is invoked under.
* `[in] js_object`: The JavaScript object to be marked.
* `[in] type_tag`: The tag with which the object is to be marked.

Returns `napi_ok` if the API succeeded.

Associates the value of the `type_tag` pointer with the JavaScript object.
`napi_check_object_type_tag()` can then be used to compare the tag that was
attached to the object with one owned by the addon to ensure that the object
has the right type.

If the object already has an associated type tag, this API will return
`napi_invalid_arg`.

