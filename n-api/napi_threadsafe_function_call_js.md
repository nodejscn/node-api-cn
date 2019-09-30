<!-- YAML
added: v10.6.0
napiVersion: 4
-->

Function pointer used with asynchronous thread-safe function calls. The callback
will be called on the main thread. Its purpose is to use a data item arriving
via the queue from one of the secondary threads to construct the parameters
necessary for a call into JavaScript, usually via `napi_call_function`, and then
make the call into JavaScript.

The data arriving from the secondary thread via the queue is given in the `data`
parameter and the JavaScript function to call is given in the `js_callback`
parameter.

N-API sets up the environment prior to calling this callback, so it is
sufficient to call the JavaScript function via `napi_call_function` rather than
via `napi_make_callback`.

Callback functions must satisfy the following signature:

```C
typedef void (*napi_threadsafe_function_call_js)(napi_env env,
                                                 napi_value js_callback,
                                                 void* context,
                                                 void* data);
```

* `[in] env`: The environment to use for API calls, or `NULL` if the thread-safe
function is being torn down and `data` may need to be freed.
* `[in] js_callback`: The JavaScript function to call, or `NULL` if the
thread-safe function is being torn down and `data` may need to be freed. It may
also be `NULL` if the thread-safe function was created without `js_callback`.
* `[in] context`: The optional data with which the thread-safe function was
created.
* `[in] data`: Data created by the secondary thread. It is the responsibility of
the callback to convert this native data to JavaScript values (with N-API
functions) that can be passed as parameters when `js_callback` is invoked. This
pointer is managed entirely by the threads and this callback. Thus this callback
should free the data.

