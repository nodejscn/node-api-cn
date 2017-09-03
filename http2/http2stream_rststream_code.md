<!-- YAML
added: v8.4.0
-->

* code {number} Unsigned 32-bit integer identifying the error code. Defaults to
  `http2.constant.NGHTTP2_NO_ERROR` (`0x00`)
* Returns: {undefined}

Sends an `RST_STREAM` frame to the connected HTTP/2 peer, causing this
`Http2Stream` to be closed on both sides using [error code][] `code`.

