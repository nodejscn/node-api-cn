<!-- YAML
added: v0.1.90
-->
* `port` {number}
* `host` {string}
* `backlog` {number} Common parameter of [`server.listen()`][] functions
* `callback` {Function} Common parameter of [`server.listen()`][] functions
* Returns: {net.Server}

Start a TCP server listening for connections on the given `port` and `host`.

If `port` is omitted or is 0, the operating system will assign an arbitrary
unused port, which can be retrieved by using `server.address().port`
after the [`'listening'`][] event has been emitted.

If `host` is omitted, the server will accept connections on the
[unspecified IPv6 address][] (`::`) when IPv6 is available, or the
[unspecified IPv4 address][] (`0.0.0.0`) otherwise.

*Note*: In most operating systems, listening to the
[unspecified IPv6 address][] (`::`) may cause the `net.Server` to also listen on
the [unspecified IPv4 address][] (`0.0.0.0`).

