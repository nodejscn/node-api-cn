
Similarly to libuv handles, thread-safe functions can be "referenced" and
"unreferenced". A "referenced" thread-safe function will cause the event loop on
the thread on which it is created to remain alive until the thread-safe function
is destroyed. In contrast, an "unreferenced" thread-safe function will not
prevent the event loop from exiting. The APIs `napi_ref_threadsafe_function` and
`napi_unref_threadsafe_function` exist for this purpose.

Neither does `napi_unref_threadsafe_function` mark the thread-safe functions as
able to be destroyed nor does `napi_ref_threadsafe_function` prevent it from
being destroyed.

