
Threads can be added to and removed from a `napi_threadsafe_function` object
during its existence. Thus, in addition to specifying an initial number of
threads upon creation, `napi_acquire_threadsafe_function` can be called to
indicate that a new thread will start making use of the thread-safe function.
Similarly, `napi_release_threadsafe_function` can be called to indicate that an
existing thread will stop making use of the thread-safe function.

`napi_threadsafe_function` objects are destroyed when every thread which uses
the object has called `napi_release_threadsafe_function()` or has received a
return status of `napi_closing` in response to a call to
`napi_call_threadsafe_function`. The queue is emptied before the
`napi_threadsafe_function` is destroyed. `napi_release_threadsafe_function()`
should be the last API call made in conjunction with a given
`napi_threadsafe_function`, because after the call completes, there is no
guarantee that the `napi_threadsafe_function` is still allocated. For the same
reason, do not make use of a thread-safe function
after receiving a return value of `napi_closing` in response to a call to
`napi_call_threadsafe_function`. Data associated with the
`napi_threadsafe_function` can be freed in its `napi_finalize` callback which
was passed to `napi_create_threadsafe_function()`. The parameter
`initial_thread_count` of `napi_create_threadsafe_function` marks the initial
number of aquisitions of the thread-safe functions, instead of calling
`napi_acquire_threadsafe_function` multiple times at creation.

Once the number of threads making use of a `napi_threadsafe_function` reaches
zero, no further threads can start making use of it by calling
`napi_acquire_threadsafe_function()`. In fact, all subsequent API calls
associated with it, except `napi_release_threadsafe_function()`, will return an
error value of `napi_closing`.

The thread-safe function can be "aborted" by giving a value of `napi_tsfn_abort`
to `napi_release_threadsafe_function()`. This will cause all subsequent APIs
associated with the thread-safe function except
`napi_release_threadsafe_function()` to return `napi_closing` even before its
reference count reaches zero. In particular, `napi_call_threadsafe_function()`
will return `napi_closing`, thus informing the threads that it is no longer
possible to make asynchronous calls to the thread-safe function. This can be
used as a criterion for terminating the thread. **Upon receiving a return value
of `napi_closing` from `napi_call_threadsafe_function()` a thread must make no
further use of the thread-safe function because it is no longer guaranteed to
be allocated.**

