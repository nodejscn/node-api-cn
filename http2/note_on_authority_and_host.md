
HTTP/2 requires requests to have either the `:authority` pseudo-header
or the `host` header. Prefer `:authority` when constructing an HTTP/2
request directly, and `host` when converting from HTTP/1 (in proxies,
for instance).

The compatibility API falls back to `host` if `:authority` is not
present. See [`request.authority`][] for more information. However,
if you don't use the compatibility API (or use `req.headers` directly),
you need to implement any fall-back behaviour yourself.




























































