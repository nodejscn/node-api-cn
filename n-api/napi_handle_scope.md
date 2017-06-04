This is an abstraction used to control and modify the lifetime of objects
created within a particular scope. In general, N-API values are created within
the context of a handle scope. When a native method is called from
JavaScript, a default handle scope will exist. If the user does not explicitly
create a new handle scope, N-API values will be created in the default handle
scope. For any invocations of code outside the execution of a native method
(for instance, during a libuv callback invocation), the module is required to
create a scope before invoking any functions that can result in the creation
of JavaScript values.

Handle scopes are created using [`napi_open_handle_scope`][] and are destroyed
using [`napi_close_handle_scope`][]. Closing the scope can indicate to the GC that
all `napi_value`s created during the lifetime of the handle scope are no longer
referenced from the current stack frame.

For more details, review the [Object Lifetime Management][].

