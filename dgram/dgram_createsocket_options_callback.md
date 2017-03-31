<!-- YAML
added: v0.11.13
-->

* `options` {Object}
* `callback` {Function} Attached as a listener to `'message'` events.
* Returns: {dgram.Socket}

Creates a `dgram.Socket` object. The `options` argument is an object that
should contain a `type` field of either `udp4` or `udp6` and an optional
boolean `reuseAddr` field.

When `reuseAddr` is `true` [`socket.bind()`][] will reuse the address, even if
another process has already bound a socket on it. `reuseAddr` defaults to
`false`. The optional `callback` function is added as a listener for `'message'`
events.

Once the socket is created, calling [`socket.bind()`][] will instruct the
socket to begin listening for datagram messages. When `address` and `port` are
not passed to  [`socket.bind()`][] the method will bind the socket to the "all
interfaces" address on a random port (it does the right thing for both `udp4`
and `udp6` sockets). The bound address and port can be retrieved using
[`socket.address().address`][] and [`socket.address().port`][].

