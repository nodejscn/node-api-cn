<!-- YAML
added: v8.0.0
napiVersion: 1
-->

```c
napi_status napi_define_class(napi_env env,
                              const char* utf8name,
                              size_t length,
                              napi_callback constructor,
                              void* data,
                              size_t property_count,
                              const napi_property_descriptor* properties,
                              napi_value* result);
```

* `[in] env`: The environment that the API is invoked under.
* `[in] utf8name`: Name of the JavaScript constructor function; When wrapping a
  C++ class, we recommend for clarity that this name be the same as that of
  the C++ class.
* `[in] length`: The length of the `utf8name` in bytes, or `NAPI_AUTO_LENGTH`
  if it is null-terminated.
* `[in] constructor`: Callback function that handles constructing instances
  of the class. When wrapping a C++ class, this method must be a static member
  with the [`napi_callback`][] signature. A C++ class constructor cannot be
  used. [`napi_callback`][] provides more details.
* `[in] data`: Optional data to be passed to the constructor callback as
  the `data` property of the callback info.
* `[in] property_count`: Number of items in the `properties` array argument.
* `[in] properties`: Array of property descriptors describing static and
  instance data properties, accessors, and methods on the class
  See `napi_property_descriptor`.
* `[out] result`: A `napi_value` representing the constructor function for
  the class.

Returns `napi_ok` if the API succeeded.

Defines a JavaScript class, including:

* A JavaScript constructor function that has the class name. When wrapping a
  corresponding C++ class, the callback passed via `constructor` can be used to
  instantiate a new C++ class instance, which can then be placed inside the
  JavaScript object instance being constructed using [`napi_wrap`][].
* Properties on the constructor function whose implementation can call
  corresponding _static_ data properties, accessors, and methods of the C++
  class (defined by property descriptors with the `napi_static` attribute).
* Properties on the constructor function's `prototype` object. When wrapping a
  C++ class, _non-static_ data properties, accessors, and methods of the C++
  class can be called from the static functions given in the property
  descriptors without the `napi_static` attribute after retrieving the C++ class
  instance placed inside the JavaScript object instance by using
  [`napi_unwrap`][].

When wrapping a C++ class, the C++ constructor callback passed via `constructor`
should be a static method on the class that calls the actual class constructor,
then wraps the new C++ instance in a JavaScript object, and returns the wrapper
object. See [`napi_wrap`][] for details.

The JavaScript constructor function returned from [`napi_define_class`][] is
often saved and used later to construct new instances of the class from native
code, and/or to check whether provided values are instances of the class. In
that case, to prevent the function value from being garbage-collected, a
strong persistent reference to it can be created using
[`napi_create_reference`][], ensuring that the reference count is kept >= 1.

Any non-`NULL` data which is passed to this API via the `data` parameter or via
the `data` field of the `napi_property_descriptor` array items can be associated
with the resulting JavaScript constructor (which is returned in the `result`
parameter) and freed whenever the class is garbage-collected by passing both
the JavaScript function and the data to [`napi_add_finalizer`][].

