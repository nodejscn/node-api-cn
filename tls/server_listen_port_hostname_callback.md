<!-- YAML
added: v0.3.2
-->

* `port` {number} The TCP/IP port on which to begin listening for connections.
  A value of `0` (zero) will assign a random port.
* `hostname` {string} The hostname, IPv4, or IPv6 address on which to begin
  listening for connections. If `undefined`, the server will accept connections
  on any IPv6 address (`::`) when IPv6 is available, or any IPv4 address
  (`0.0.0.0`) otherwise.
* `callback` {Function} A callback function to be invoked when the server has
  begun listening on the `port` and `hostname`.

The `server.listen()` methods instructs the server to begin accepting
connections on the specified `port` and `hostname`.

This function operates asynchronously. If the `callback` is given, it will be
called when the server has started listening.

See [`net.Server`][] for more information.

