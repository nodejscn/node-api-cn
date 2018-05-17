<!-- YAML
added: v8.4.0
-->
- `callback` {Function}

Stops the server from accepting new connections.  See [`net.Server.close()`][].

Note that this is not analogous to restricting new requests since HTTP/2
connections are persistent. To achieve a similar graceful shutdown behavior,
consider also using [`http2session.close()`] on active sessions.

