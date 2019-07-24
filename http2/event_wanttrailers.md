<!-- YAML
added: v10.0.0
-->

The `'wantTrailers'` event is emitted when the `Http2Stream` has queued the
final `DATA` frame to be sent on a frame and the `Http2Stream` is ready to send
trailing headers. When initiating a request or response, the `waitForTrailers`
option must be set for this event to be emitted.

