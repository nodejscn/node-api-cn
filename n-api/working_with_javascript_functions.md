
Node-API provides a set of APIs that allow JavaScript code to
call back into native code. Node-APIs that support calling back
into native code take in a callback functions represented by
the `napi_callback` type. When the JavaScript VM calls back to
native code, the `napi_callback` function provided is invoked. The APIs
documented in this section allow the callback function to do the
following:

* Get information about the context in which the callback was invoked.
* Get the arguments passed into the callback.
* Return a `napi_value` back from the callback.

Additionally, Node-API provides a set of functions which allow calling
JavaScript functions from native code. One can either call a function
like a regular JavaScript function call, or as a constructor
function.

Any non-`NULL` data which is passed to this API via the `data` field of the
`napi_property_descriptor` items can be associated with `object` and freed
whenever `object` is garbage-collected by passing both `object` and the data to
[`napi_add_finalizer`][].

