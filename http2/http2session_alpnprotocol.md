<!-- YAML
added: v9.4.0
-->

* {string|undefined}

Value will be `undefined` if the `Http2Session` is not yet connected to a
socket, `h2c` if the `Http2Session` is not connected to a `TLSSocket`, or
will return the value of the connected `TLSSocket`'s own `alpnProtocol`
property.

