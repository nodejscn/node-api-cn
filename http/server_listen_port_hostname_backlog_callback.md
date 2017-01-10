<!-- YAML
added: v0.1.90
-->

* `port` {Number}
* `hostname` {String}
* `backlog` {Number}
* `callback` {Function}

Begin accepting connections on the specified `port` and `hostname`. If the
`hostname` is omitted, the server will accept connections on any IPv6 address
(`::`) when IPv6 is available, or any IPv4 address (`0.0.0.0`) otherwise.
Omit the port argument, or use a port value of `0`, to have the operating system
assign a random port, which can be retrieved by using `server.address().port`
after the `'listening'` event has been emitted.

To listen to a unix socket, supply a filename instead of port and hostname.

`backlog` is the maximum length of the queue of pending connections.
The actual length will be determined by your OS through sysctl settings such as
`tcp_max_syn_backlog` and `somaxconn` on linux. The default value of this
parameter is 511 (not 512).

This function is asynchronous. `callback` will be added as a listener for the
[`'listening'`][] event.  See also [`net.Server.listen(port)`][].

*Note*: The `server.listen()` method may be called multiple times. Each
subsequent call will *re-open* the server using the provided options.

