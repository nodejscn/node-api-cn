
<!-- YAML
added: v8.0.0
napiVersion: 5
-->

```c
napi_status napi_add_finalizer(napi_env env,
                               napi_value js_object,
                               void* native_object,
                               napi_finalize finalize_cb,
                               void* finalize_hint,
                               napi_ref* result);
```

* `[in] env`: The environment that the API is invoked under.
* `[in] js_object`: The JavaScript object to which the native data will be
  attached.
* `[in] native_object`: The native data that will be attached to the JavaScript
  object.
* `[in] finalize_cb`: Native callback that will be used to free the
  native data when the JavaScript object is ready for garbage-collection.
  [`napi_finalize`][] provides more details.
* `[in] finalize_hint`: Optional contextual hint that is passed to the
  finalize callback.
* `[out] result`: Optional reference to the JavaScript object.

Returns `napi_ok` if the API succeeded.

Adds a `napi_finalize` callback which will be called when the JavaScript object
in `js_object` is ready for garbage collection. This API is similar to
`napi_wrap()` except that:

* the native data cannot be retrieved later using `napi_unwrap()`,
* nor can it be removed later using `napi_remove_wrap()`, and
* the API can be called multiple times with different data items in order to
  attach each of them to the JavaScript object, and
* the object manipulated by the API can be used with `napi_wrap()`.

*Caution*: The optional returned reference (if obtained) should be deleted via
[`napi_delete_reference`][] ONLY in response to the finalize callback
invocation. If it is deleted before then, then the finalize callback may never
be invoked. Therefore, when obtaining a reference a finalize callback is also
required in order to enable correct disposal of the reference.

