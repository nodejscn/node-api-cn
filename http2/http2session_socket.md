<!-- YAML
added: v8.4.0
-->

* Value: {net.Socket|tls.TLSSocket}

Returns a Proxy object that acts as a `net.Socket` (or `tls.TLSSocket`) but
limits available methods to ones safe to use with HTTP/2.

`destroy`, `emit`, `end`, `pause`, `read`, `resume`, and `write` will throw
an error with code `ERR_HTTP2_NO_SOCKET_MANIPULATION`. See
[Http2Session and Sockets][] for more information.

`setTimeout` method will be called on this `Http2Session`.

All other interactions will be routed directly to the socket.

