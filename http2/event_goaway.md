<!-- YAML
added: v8.4.0
-->

* `errorCode` {number} The HTTP/2 error code specified in the `GOAWAY` frame.
* `lastStreamID` {number} The ID of the last stream the remote peer successfully
  processed (or `0` if no ID is specified).
* `opaqueData` {Buffer} If additional opaque data was included in the `GOAWAY`
  frame, a `Buffer` instance will be passed containing that data.

The `'goaway'` event is emitted when a `GOAWAY` frame is received.

The `Http2Session` instance will be shut down automatically when the `'goaway'`
event is emitted.

