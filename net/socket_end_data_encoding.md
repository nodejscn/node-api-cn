<!-- YAML
added: v0.1.90
-->

* Returns: {net.Socket} The socket itself.

Half-closes the socket. i.e., it sends a FIN packet. It is possible the
server will still send some data.

If `data` is specified, it is equivalent to calling
`socket.write(data, encoding)` followed by [`socket.end()`][].

