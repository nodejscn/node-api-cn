<!-- YAML
added: v0.1.90
-->

Opens the connection for a given socket.

For TCP sockets, `options` argument should be an object which specifies:

  - `port`: Port the client should connect to (Required).

  - `host`: Host the client should connect to. Defaults to `'localhost'`.

  - `localAddress`: Local interface to bind to for network connections.

  - `localPort`: Local port to bind to for network connections.

  - `family` : Version of IP stack. Defaults to `4`.

  - `hints`: [`dns.lookup()` hints][]. Defaults to `0`.

  - `lookup` : Custom lookup function. Defaults to `dns.lookup`.

For local domain sockets, `options` argument should be an object which
specifies:

  - `path`: Path the client should connect to (Required).

Normally this method is not needed, as `net.createConnection` opens the
socket. Use this only if you are implementing a custom Socket.

This function is asynchronous. When the [`'connect'`][] event is emitted the
socket is established. If there is a problem connecting, the `'connect'` event
will not be emitted, the [`'error'`][] event will be emitted with the exception.

The `connectListener` parameter will be added as a listener for the
[`'connect'`][] event.

