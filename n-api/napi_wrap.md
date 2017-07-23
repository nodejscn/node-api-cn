<!-- YAML
added: v8.0.0
-->
```C
napi_status napi_wrap(napi_env env,
                      napi_value js_object,
                      void* native_object,
                      napi_finalize finalize_cb,
                      void* finalize_hint,
                      napi_ref* result);
```

 - `[in] env`: The environment that the API is invoked under.
 - `[in] js_object`: The JavaScript object that will be the wrapper for the
   native object. This object _must_ have been created from the `prototype` of
   a constructor that was created using `napi_define_class()`.
 - `[in] native_object`: The native instance that will be wrapped in the
   JavaScript object.
 - `[in] finalize_cb`: Optional native callback that can be used to free the
   native instance when the JavaScript object is ready for garbage-collection.
 - `[in] finalize_hint`: Optional contextual hint that is passed to the
   finalize callback.
 - `[out] result`: Optional reference to the wrapped object.

Returns `napi_ok` if the API succeeded.

Wraps a native instance in a JavaScript object. The native instance can be
retrieved later using `napi_unwrap()`.

When JavaScript code invokes a constructor for a class that was defined using
`napi_define_class()`, the `napi_callback` for the constructor is invoked.
After constructing an instance of the native class, the callback must then call
`napi_wrap()` to wrap the newly constructed instance in the already-created
JavaScript object that is the `this` argument to the constructor callback.
(That `this` object was created from the constructor function's `prototype`,
so it already has definitions of all the instance properties and methods.)

Typically when wrapping a class instance, a finalize callback should be
provided that simply deletes the native instance that is received as the `data`
argument to the finalize callback.

The optional returned reference is initially a weak reference, meaning it
has a reference count of 0. Typically this reference count would be incremented
temporarily during async operations that require the instance to remain valid.

*Caution*: The optional returned reference (if obtained) should be deleted via
[`napi_delete_reference`][] ONLY in response to the finalize callback
invocation. (If it is deleted before then, then the finalize callback may never
be invoked.) Therefore, when obtaining a reference a finalize callback is also
required in order to enable correct proper of the reference.

*Note*: This API may modify the prototype chain of the wrapper object.
Afterward, additional manipulation of the wrapper's prototype chain may cause
`napi_unwrap()` to fail.

*Note*: Calling `napi_wrap()` a second time on an object that already has a
native instance associated with it by virtue of a previous call to
`napi_wrap()` will cause an error to be returned.

