<!-- YAML
added: v14.10.0
-->

An opaque value returned by [`napi_add_async_cleanup_hook`][]. It must be passed
to [`napi_remove_async_cleanup_hook`][] when the chain of asynchronous cleanup
events completes.

