<!-- YAML
added: v8.4.0
-->

* Value: {net.Socket|tls.TLSSocket}

A reference to the [`net.Socket`][] or [`tls.TLSSocket`][] to which this
`Http2Session` instance is bound.

*Note*: It is not recommended for user code to interact directly with a
`Socket` bound to an `Http2Session`. See [Http2Session and Sockets][] for
details.

