<!-- YAML
added: v0.5.10
-->

* `handle` {Object}
* `callback` {Function}

The `handle` object can be set to either a server or socket (anything
with an underlying `_handle` member), or a `{fd: <n>}` object.

This will cause the server to accept connections on the specified
handle, but it is presumed that the file descriptor or handle has
already been bound to a port or domain socket.

Listening on a file descriptor is not supported on Windows.

This function is asynchronous. `callback` will be added as a listener for the
[`'listening'`][] event. See also [`net.Server.listen()`][].

Returns `server`.

*Note*: The `server.listen()` method may be called multiple times. Each
subsequent call will *re-open* the server using the provided options.

