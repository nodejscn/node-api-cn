<!-- YAML
added: v0.1.90
changes:
  - version: v6.0.0
    pr-url: https://github.com/nodejs/node/pull/6021
    description: The `hints` option defaults to `0` in all cases now.
                 Previously, in the absence of the `family` option it would
                 default to `dns.ADDRCONFIG | dns.V4MAPPED`.
  - version: v5.11.0
    pr-url: https://github.com/nodejs/node/pull/6000
    description: The `hints` option is supported now.
-->

* `options` {Object}
* `connectListener` {Function} Common parameter of [`socket.connect()`][]
  methods. Will be added as a listener for the [`'connect'`][] event once.
* Returns: {net.Socket} The socket itself.

Initiate a connection on a given socket. Normally this method is not needed,
the socket should be created and opened with [`net.createConnection()`][]. Use
this only when implementing a custom Socket.

For TCP connections, available `options` are:

* `port` {number} Required. Port the socket should connect to.
* `host` {string} Host the socket should connect to. Defaults to `'localhost'`.
* `localAddress` {string} Local address the socket should connect from.
* `localPort` {number} Local port the socket should connect from.
* `family` {number}: Version of IP stack, can be either 4 or 6. Defaults to 4.
* `hints` {number} Optional [`dns.lookup()` hints][].
* `lookup` {Function} Custom lookup function. Defaults to [`dns.lookup()`][].

For [IPC][] connections, available `options` are:

* `path` {string} Required. Path the client should connect to.
  See [Identifying paths for IPC connections][].

Returns `socket`.

