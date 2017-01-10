<!-- YAML
added: v0.1.90
-->

* `path` {String}
* `callback` {Function}

Start a UNIX socket server listening for connections on the given `path`.

This function is asynchronous. `callback` will be added as a listener for the
[`'listening'`][] event.  See also [`net.Server.listen(path)`][].

*Note*: The `server.listen()` method may be called multiple times. Each
subsequent call will *re-open* the server using the provided options.

