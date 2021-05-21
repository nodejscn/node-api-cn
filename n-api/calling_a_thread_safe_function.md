
`napi_call_threadsafe_function()` can be used for initiating a call into
JavaScript. `napi_call_threadsafe_function()` accepts a parameter which controls
whether the API behaves blockingly. If set to `napi_tsfn_nonblocking`, the API
behaves non-blockingly, returning `napi_queue_full` if the queue was full,
preventing data from being successfully added to the queue. If set to
`napi_tsfn_blocking`, the API blocks until space becomes available in the queue.
`napi_call_threadsafe_function()` never blocks if the thread-safe function was
created with a maximum queue size of 0.

`napi_call_threadsafe_function()` should not be called with `napi_tsfn_blocking`
from a JavaScript thread, because, if the queue is full, it may cause the
JavaScript thread to deadlock.

The actual call into JavaScript is controlled by the callback given via the
`call_js_cb` parameter. `call_js_cb` is invoked on the main thread once for each
value that was placed into the queue by a successful call to
`napi_call_threadsafe_function()`. If such a callback is not given, a default
callback will be used, and the resulting JavaScript call will have no arguments.
The `call_js_cb` callback receives the JavaScript function to call as a
`napi_value` in its parameters, as well as the `void*` context pointer used when
creating the `napi_threadsafe_function`, and the next data pointer that was
created by one of the secondary threads. The callback can then use an API such
as `napi_call_function()` to call into JavaScript.

The callback may also be invoked with `env` and `call_js_cb` both set to `NULL`
to indicate that calls into JavaScript are no longer possible, while items
remain in the queue that may need to be freed. This normally occurs when the
Node.js process exits while there is a thread-safe function still active.

It is not necessary to call into JavaScript via `napi_make_callback()` because
Node-API runs `call_js_cb` in a context appropriate for callbacks.

