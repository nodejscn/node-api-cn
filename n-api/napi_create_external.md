<!-- YAML
added: v8.0.0
napiVersion: 1
-->

```c
napi_status napi_create_external(napi_env env,
                                 void* data,
                                 napi_finalize finalize_cb,
                                 void* finalize_hint,
                                 napi_value* result)
```

* `[in] env`: The environment that the API is invoked under.
* `[in] data`: Raw pointer to the external data.
* `[in] finalize_cb`: Optional callback to call when the external value is being
  collected.
* `[in] finalize_hint`: Optional hint to pass to the finalize callback during
  collection.
* `[out] result`: A `napi_value` representing an external value.

Returns `napi_ok` if the API succeeded.

This API allocates a JavaScript value with external data attached to it. This
is used to pass external data through JavaScript code, so it can be retrieved
later by native code using [`napi_get_value_external`][].

The API adds a `napi_finalize` callback which will be called when the JavaScript
object just created is ready for garbage collection. It is similar to
`napi_wrap()` except that:

* the native data cannot be retrieved later using `napi_unwrap()`,
* nor can it be removed later using `napi_remove_wrap()`, and
* the object created by the API can be used with `napi_wrap()`.

The created value is not an object, and therefore does not support additional
properties. It is considered a distinct value type: calling `napi_typeof()` with
an external value yields `napi_external`.

