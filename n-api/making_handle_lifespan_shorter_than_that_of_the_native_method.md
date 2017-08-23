It is often necessary to make the lifespan of handles shorter than
the lifespan of a native method. For example, consider a native method
that has a loop which iterates through the elements in a large array:

```C
for (int i = 0; i < 1000000; i++) {
  napi_value result;
  napi_status status = napi_get_element(e object, i, &result);
  if (status != napi_ok) {
    break;
  }
  // do something with element
}
```

This would result in a large number of handles being created, consuming
substantial resources. In addition, even though the native code could only
use the most recent handle, all of the associated objects would also be
kept alive since they all share the same scope.

To handle this case, N-API provides the ability to establish a new 'scope' to
which newly created handles will be associated. Once those handles
are no longer required, the scope can be 'closed' and any handles associated
with the scope are invalidated. The methods available to open/close scopes are
[`napi_open_handle_scope`][] and [`napi_close_handle_scope`][].

N-API only supports a single nested hiearchy of scopes. There is only one
active scope at any time, and all new handles will be associated with that
scope while it is active. Scopes must be closed in the reverse order from
which they are opened. In addition, all scopes created within a native method
must be closed before returning from that method.

Taking the earlier example, adding calls to [`napi_open_handle_scope`][] and
[`napi_close_handle_scope`][] would ensure that at most a single handle
is valid throughout the execution of the loop:

```C
for (int i = 0; i < 1000000; i++) {
  napi_handle_scope scope;
  napi_status status = napi_open_handle_scope(env, &scope);
  if (status != napi_ok) {
    break;
  }
  napi_value result;
  status = napi_get_element(e object, i, &result);
  if (status != napi_ok) {
    break;
  }
  // do something with element
  status = napi_close_handle_scope(env, scope);
  if (status != napi_ok) {
    break;
  }
}
```

When nesting scopes, there are cases where a handle from an
inner scope needs to live beyond the lifespan of that scope. N-API supports an
'escapable scope' in order to support this case. An escapable scope
allows one handle to be 'promoted' so that it 'escapes' the
current scope and the lifespan of the handle changes from the current
scope to that of the outer scope.

The methods available to open/close escapable scopes are
[`napi_open_escapable_handle_scope`][] and [`napi_close_escapable_handle_scope`][].

The request to promote a handle is made through [`napi_escape_handle`][] which
can only be called once.

