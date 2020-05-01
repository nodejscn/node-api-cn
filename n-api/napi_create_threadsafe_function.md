
<!-- YAML
added: v10.6.0
napiVersion: 4
changes:
  - version:
     - v12.6.0
     - v10.17.0
    pr-url: https://github.com/nodejs/node/pull/27791
    description: Made `func` parameter optional with custom `call_js_cb`.
-->

```C
NAPI_EXTERN napi_status
napi_create_threadsafe_function(napi_env env,
                                napi_value func,
                                napi_value async_resource,
                                napi_value async_resource_name,
                                size_t max_queue_size,
                                size_t initial_thread_count,
                                void* thread_finalize_data,
                                napi_finalize thread_finalize_cb,
                                void* context,
                                napi_threadsafe_function_call_js call_js_cb,
                                napi_threadsafe_function* result);
```

* `[in] env`: The environment that the API is invoked under.
* `[in] func`: An optional JavaScript function to call from another thread. It
  must be provided if `NULL` is passed to `call_js_cb`.
* `[in] async_resource`: An optional object associated with the async work that
  will be passed to possible `async_hooks` [`init` hooks][].
* `[in] async_resource_name`: A JavaScript string to provide an identifier for
  the kind of resource that is being provided for diagnostic information exposed
  by the `async_hooks` API.
* `[in] max_queue_size`: Maximum size of the queue. `0` for no limit.
* `[in] initial_thread_count`: The initial number of threads, including the main
  thread, which will be making use of this function.
* `[in] thread_finalize_data`: Optional data to be passed to `thread_finalize_cb`.
* `[in] thread_finalize_cb`: Optional function to call when the
  `napi_threadsafe_function` is being destroyed.
* `[in] context`: Optional data to attach to the resulting
  `napi_threadsafe_function`.
* `[in] call_js_cb`: Optional callback which calls the JavaScript function in
  response to a call on a different thread. This callback will be called on the
  main thread. If not given, the JavaScript function will be called with no
  parameters and with `undefined` as its `this` value.
* `[out] result`: The asynchronous thread-safe JavaScript function.

