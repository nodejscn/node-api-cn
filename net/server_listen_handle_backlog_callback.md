<!-- YAML
added: v0.5.10
-->

* `handle` {Object}
* `backlog` {Number}
* `callback` {Function}

The `handle` object can be set to either a server or socket (anything
with an underlying `_handle` member), or a `{fd: <n>}` object.

This will cause the server to accept connections on the specified
handle, but it is presumed that the file descriptor or handle has
already been bound to a port or domain socket.

Listening on a file descriptor is not supported on Windows.

This function is asynchronous.  When the server has been bound,
[`'listening'`][] event will be emitted.
The last parameter `callback` will be added as a listener for the
[`'listening'`][] event.

The parameter `backlog` behaves the same as in
[`server.listen([port][, hostname][, backlog][, callback])`][`server.listen(port, host, backlog, callback)`].

