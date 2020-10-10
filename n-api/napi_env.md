
`napi_env` is used to represent a context that the underlying N-API
implementation can use to persist VM-specific state. This structure is passed
to native functions when they're invoked, and it must be passed back when
making N-API calls. Specifically, the same `napi_env` that was passed in when
the initial native function was called must be passed to any subsequent
nested N-API calls. Caching the `napi_env` for the purpose of general reuse,
and passing the `napi_env` between instances of the same addon running on
different [`Worker`][] threads is not allowed. The `napi_env` becomes invalid
when an instance of a native addon is unloaded. Notification of this event is
delivered through the callbacks given to [`napi_add_env_cleanup_hook`][] and
[`napi_set_instance_data`][].

