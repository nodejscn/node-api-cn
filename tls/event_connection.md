<!-- YAML
added: v0.3.2
-->

* `socket` {stream.Duplex}

This event is emitted when a new TCP stream is established, before the TLS
handshake begins. `socket` is typically an object of type [`net.Socket`][].
Usually users will not want to access this event.

This event can also be explicitly emitted by users to inject connections
into the TLS server. In that case, any [`Duplex`][] stream can be passed.

