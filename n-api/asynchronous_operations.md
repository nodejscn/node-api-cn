
Addon modules often need to leverage async helpers from libuv as part of their
implementation. This allows them to schedule work to be executed asynchronously
so that their methods can return in advance of the work being completed. This
is important in order to allow them to avoid blocking overall execution
of the Node.js application.

N-API provides an ABI-stable interface for these
supporting functions which covers the most common asynchronous use cases.

N-API defines the `napi_work` structure which is used to manage
asynchronous workers. Instances are created/deleted with
[`napi_create_async_work`][] and [`napi_delete_async_work`][].

The `execute` and `complete` callbacks are functions that will be
invoked when the executor is ready to execute and when it completes its
task respectively. These functions implement the following interfaces:

```C
typedef void (*napi_async_execute_callback)(napi_env env,
                                            void* data);
typedef void (*napi_async_complete_callback)(napi_env env,
                                             napi_status status,
                                             void* data);
```


When these methods are invoked, the `data` parameter passed will be the
addon-provided void* data that was passed into the
`napi_create_async_work` call.

Once created the async worker can be queued
for execution using the [`napi_queue_async_work`][] function:

```C
NAPI_EXTERN napi_status napi_queue_async_work(napi_env env,
                                              napi_async_work work);
```

[`napi_cancel_async_work`][] can be used if  the work needs
to be cancelled before the work has started execution.

After calling [`napi_cancel_async_work`][], the `complete` callback
will be invoked with a status value of `napi_cancelled`.
The work should not be deleted before the `complete`
callback invocation, even when it was cancelled.

