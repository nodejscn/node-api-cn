<!-- YAML
added: v8.4.0
-->

* `code` {number} Unsigned 32-bit integer identifying the error code.
  **Default:** `http2.constants.NGHTTP2_NO_ERROR` (`0x00`).
* `callback` {Function} An optional function registered to listen for the
  `'close'` event.

Closes the `Http2Stream` instance by sending an `RST_STREAM` frame to the
connected HTTP/2 peer.

