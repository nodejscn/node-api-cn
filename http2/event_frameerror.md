<!-- YAML
added: v8.4.0
-->

* `type` {integer} The frame type.
* `code` {integer} The error code.
* `id` {integer} The stream id (or `0` if the frame isn't associated with a
  stream).

The `'frameError'` event is emitted when an error occurs while attempting to
send a frame on the session. If the frame that could not be sent is associated
with a specific `Http2Stream`, an attempt to emit a `'frameError'` event on the
`Http2Stream` is made.

If the `'frameError'` event is associated with a stream, the stream will be
closed and destroyed immediately following the `'frameError'` event. If the
event is not associated with a stream, the `Http2Session` will be shut down
immediately following the `'frameError'` event.

