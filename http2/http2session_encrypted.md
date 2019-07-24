<!-- YAML
added: v9.4.0
-->

* {boolean|undefined}

Value is `undefined` if the `Http2Session` session socket has not yet been
connected, `true` if the `Http2Session` is connected with a `TLSSocket`,
and `false` if the `Http2Session` is connected to any other kind of socket
or stream.

