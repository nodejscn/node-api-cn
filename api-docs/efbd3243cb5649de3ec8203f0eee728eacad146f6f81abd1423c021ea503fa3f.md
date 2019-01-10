
N-API provides facilities for creating `Promise` objects as described in
[Section 25.4][] of the ECMA specification. It implements promises as a pair of
objects. When a promise is created by `napi_create_promise()`, a "deferred"
object is created and returned alongside the `Promise`. The deferred object is
bound to the created `Promise` and is the only means to resolve or reject the
`Promise` using `napi_resolve_deferred()` or `napi_reject_deferred()`. The
deferred object that is created by `napi_create_promise()` is freed by
`napi_resolve_deferred()` or `napi_reject_deferred()`. The `Promise` object may
be returned to JavaScript where it can be used in the usual fashion.

For example, to create a promise and pass it to an asynchronous worker:
```c
napi_deferred deferred;
napi_value promise;
napi_status status;

// Create the promise.
status = napi_create_promise(env, &deferred, &promise);
if (status != napi_ok) return NULL;

// Pass the deferred to a function that performs an asynchronous action.
do_something_asynchronous(deferred);

// Return the promise to JS
return promise;
```

The above function `do_something_asynchronous()` would perform its asynchronous
action and then it would resolve or reject the deferred, thereby concluding the
promise and freeing the deferred:
```c
napi_deferred deferred;
napi_value undefined;
napi_status status;

// Create a value with which to conclude the deferred.
status = napi_get_undefined(env, &undefined);
if (status != napi_ok) return NULL;

// Resolve or reject the promise associated with the deferred depending on
// whether the asynchronous action succeeded.
if (asynchronous_action_succeeded) {
  status = napi_resolve_deferred(env, deferred, undefined);
} else {
  status = napi_reject_deferred(env, deferred, undefined);
}
if (status != napi_ok) return NULL;

// At this point the deferred has been freed, so we should assign NULL to it.
deferred = NULL;
```

