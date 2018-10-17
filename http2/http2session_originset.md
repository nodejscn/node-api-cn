<!-- YAML
added: v9.4.0
-->

* {string[]|undefined}

If the `Http2Session` is connected to a `TLSSocket`, the `originSet` property
will return an `Array` of origins for which the `Http2Session` may be
considered authoritative.

The `originSet` property is only available when using a secure TLS connection.

