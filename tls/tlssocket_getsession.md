<!-- YAML
added: v0.11.4
-->

* {Buffer}

Returns the TLS session data or `undefined` if no session was
negotiated. On the client, the data can be provided to the `session` option of
[`tls.connect()`][] to resume the connection. On the server, it may be useful
for debugging.

See [Session Resumption][] for more information.

Note: `getSession()` works only for TLSv1.2 and below. For TLSv1.3, applications
must use the [`'session'`][] event (it also works for TLSv1.2 and below).

