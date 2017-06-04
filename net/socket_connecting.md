<!-- YAML
added: v6.1.0
-->

If `true` -
[`socket.connect(options[, connectListener])`][`socket.connect(options)`]
was called and haven't yet finished. Will be set to `false` before emitting
`connect` event and/or calling
[`socket.connect(options[, connectListener])`][`socket.connect(options)`]'s
callback.

