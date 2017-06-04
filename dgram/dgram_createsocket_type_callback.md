<!-- YAML
added: v0.1.99
-->

* `type` {string} - Either 'udp4' or 'udp6'
* `callback` {Function} - Attached as a listener to `'message'` events.
  Optional
* Returns: {dgram.Socket}

Creates a `dgram.Socket` object of the specified `type`. The `type` argument
can be either `udp4` or `udp6`. An optional `callback` function can be passed
which is added as a listener for `'message'` events.

Once the socket is created, calling [`socket.bind()`][] will instruct the
socket to begin listening for datagram messages. When `address` and `port` are
not passed to  [`socket.bind()`][] the method will bind the socket to the "all
interfaces" address on a random port (it does the right thing for both `udp4`
and `udp6` sockets). The bound address and port can be retrieved using
[`socket.address().address`][] and [`socket.address().port`][].

[`'close'`]: #dgram_event_close
[`Error`]: errors.html#errors_class_error
[`EventEmitter`]: events.html
[`close()`]: #dgram_socket_close_callback
[`cluster`]: cluster.html
[`dgram.Socket#bind()`]: #dgram_socket_bind_options_callback
[`dgram.createSocket()`]: #dgram_dgram_createsocket_options_callback
[`socket.address().address`]: #dgram_socket_address
[`socket.address().port`]: #dgram_socket_address
[`socket.bind()`]: #dgram_socket_bind_port_address_callback
[byte length]: buffer.html#buffer_class_method_buffer_bytelength_string_encoding
