<!-- YAML
added: v0.11.13
changes:
  - version: v8.6.0
    pr-url: https://github.com/nodejs/node/pull/14560
    description: The `lookup` option is supported.
  - version: v8.7.0
    pr-url: https://github.com/nodejs/node/pull/13623
    description: The `recvBufferSize` and `sendBufferSize` options are
                 supported now.
-->

* `options` {Object} Available options are:
  * `type` {string} The family of socket. Must be either `'udp4'` or `'udp6'`.
    Required.
  * `reuseAddr` {boolean} When `true` [`socket.bind()`][] will reuse the
    address, even if another process has already bound a socket on it.
    Defaults to `false`.
  * `recvBufferSize` {number} - Sets the `SO_RCVBUF` socket value.
  * `sendBufferSize` {number} - Sets the `SO_SNDBUF` socket value.
  * `lookup` {Function} Custom lookup function. Defaults to [`dns.lookup()`][].
* `callback` {Function} Attached as a listener for `'message'` events. Optional.
* Returns: {dgram.Socket}

Creates a `dgram.Socket` object. Once the socket is created, calling
[`socket.bind()`][] will instruct the socket to begin listening for datagram
messages. When `address` and `port` are not passed to  [`socket.bind()`][] the
method will bind the socket to the "all interfaces" address on a random port
(it does the right thing for both `udp4` and `udp6` sockets). The bound address
and port can be retrieved using [`socket.address().address`][] and
[`socket.address().port`][].
