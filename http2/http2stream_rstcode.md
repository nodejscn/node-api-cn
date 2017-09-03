<!-- YAML
added: v8.4.0
-->

* Value: {number}

Set to the `RST_STREAM` [error code][] reported when the `Http2Stream` is
destroyed after either receiving an `RST_STREAM` frame from the connected peer,
calling `http2stream.rstStream()`, or `http2stream.destroy()`. Will be
`undefined` if the `Http2Stream` has not been closed.

