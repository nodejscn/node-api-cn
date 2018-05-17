<!-- YAML
added: v8.4.0
-->

Call [`http2stream.pushStream()`][] with the given headers, and wraps the
given newly created [`Http2Stream`] on `Http2ServerRespose`.

The callback will be called with an error with code `ERR_HTTP2_STREAM_CLOSED`
if the stream is closed.

