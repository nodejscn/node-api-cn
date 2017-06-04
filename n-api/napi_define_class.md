<!-- YAML
added: v8.0.0
-->
```C
napi_status napi_define_class(napi_env env,
                              const char* utf8name,
                              napi_callback constructor,
                              void* data,
                              size_t property_count,
                              const napi_property_descriptor* properties,
                              napi_value* result);
```

 - `[in] env`: The environment that the API is invoked under.
 - `[in] utf8name`: Name of the JavaScript constructor function; this is
   not required to be the same as the C++ class name, though it is recommended
   for clarity.
 - `[in] constructor`: Callback function that handles constructing instances
   of the class. (This should be a static method on the class, not an actual
   C++ constructor function.)
 - `[in] data`: Optional data to be passed to the constructor callback as
   the `data` property of the callback info.
 - `[in] property_count`: Number of items in the `properties` array argument.
 - `[in] properties`: Array of property descriptors describing static and
   instance data properties, accessors, and methods on the class
   See `napi_property_descriptor`.
 - `[out] result`: A `napi_value` representing the constructor function for
   the class.

Returns `napi_ok` if the API succeeded.

Defines a JavaScript class that corresponds to a C++ class, including:
 - A JavaScript constructor function that has the class name and invokes the
   provided C++ constructor callback.
 - Properties on the constructor function corresponding to _static_ data
   properties, accessors, and methods of the C++ class (defined by
   property descriptors with the `napi_static` attribute).
 - Properties on the constructor function's `prototype` object corresponding to
   _non-static_ data properties, accessors, and methods of the C++ class
   (defined by property descriptors without the `napi_static` attribute).

The C++ constructor callback should be a static method on the class that calls
the actual class constructor, then wraps the new C++ instance in a JavaScript
object, and returns the wrapper object. See `napi_wrap()` for details.

The JavaScript constructor function returned from [`napi_define_class`][] is
often saved and used later, to construct new instances of the class from native
code, and/or check whether provided values are instances of the class. In that
case, to prevent the function value from being garbage-collected, create a
persistent reference to it using [`napi_create_reference`][] and ensure the
reference count is kept >= 1.

