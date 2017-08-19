<!-- YAML
added: v8.4.0
-->

The `'streamClosed'` event is emitted when the `Http2Stream` is destroyed. Once
this event is emitted, the `Http2Stream` instance is no longer usable.

The listener callback is passed a single argument specifying the HTTP/2 error
code specified when closing the stream. If the code is any value other than
`NGHTTP2_NO_ERROR` (`0`), an `'error'` event will also be emitted.

