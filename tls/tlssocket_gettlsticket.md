<!-- YAML
added: v0.11.4
-->

Returns the TLS session ticket or `undefined` if no session was negotiated.

*Note*: This only works with client TLS sockets. Useful only for debugging,
for session reuse provide `session` option to [`tls.connect()`][].

