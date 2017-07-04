<!-- YAML
added: v0.1.90
-->

* `port` {number} Port the client should connect to.
* `host` {string} Host the client should connect to.
* `connectListener` {Function} Common parameter of [`socket.connect()`][]
  methods. Will be added as a listener for the [`'connect'`][] event once.
* Returns: {net.Socket} The socket itself.

Initiate a TCP connection on the given socket.

Alias to
[`socket.connect(options[, connectListener])`][`socket.connect(options)`]
called with `{port: port, host: host}` as `options`.

Returns `socket`.

