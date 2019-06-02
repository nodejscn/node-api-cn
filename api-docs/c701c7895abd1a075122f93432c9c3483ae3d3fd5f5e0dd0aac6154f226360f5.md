<!-- YAML
added: v0.11.4
-->

* {Buffer}

Returns the TLS session data or `undefined` if no session was
negotiated. On the client, the data can be provided to the `session` option of
[`tls.connect()`][] to resume the connection. On the server, it may be useful
for debugging.

See [Session Resumption][] for more information.

