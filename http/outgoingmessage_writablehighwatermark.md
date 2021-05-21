<!-- YAML
added: v13.0.0
-->

* {number}

This `outgoingMessage.writableHighWaterMark` will be the `highWaterMark` of
underlying socket if socket exists. Else, it would be the default
`highWaterMark`.

`highWaterMark` is the maximum amount of data that can be potentially
buffered by the socket.

