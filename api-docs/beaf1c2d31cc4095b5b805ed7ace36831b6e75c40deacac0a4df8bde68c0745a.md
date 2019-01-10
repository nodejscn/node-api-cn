`napi_env` is used to represent a context that the underlying N-API
implementation can use to persist VM-specific state. This structure is passed
to native functions when they're invoked, and it must be passed back when
making N-API calls. Specifically, the same `napi_env` that was passed in when
the initial native function was called must be passed to any subsequent
nested N-API calls. Caching the `napi_env` for the purpose of general reuse is
not allowed.

