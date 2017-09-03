<!-- YAML
added: v8.4.0
-->

The `'frameError'` event is emitted when an error occurs while attempting to
send a frame on the session. If the frame that could not be sent is associated
with a specific `Http2Stream`, an attempt to emit `'frameError'` event on the
`Http2Stream` is made.

When invoked, the handler function will receive three arguments:

* An integer identifying the frame type.
* An integer identifying the error code.
* An integer identifying the stream (or 0 if the frame is not associated with
  a stream).

If the `'frameError'` event is associated with a stream, the stream will be
closed and destroyed immediately following the `'frameError'` event. If the
event is not associated with a stream, the `Http2Session` will be shutdown
immediately following the `'frameError'` event.

