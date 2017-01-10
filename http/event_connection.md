<!-- YAML
added: v0.1.0
-->

* `socket` {net.Socket}

When a new TCP stream is established. `socket` is an object of type
[`net.Socket`][]. Usually users will not want to access this event. In
particular, the socket will not emit `'readable'` events because of how
the protocol parser attaches to the socket. The `socket` can also be
accessed at `request.connection`.

