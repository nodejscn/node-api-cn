<!-- YAML
added: v8.4.0
-->

Provides miscellaneous information about the current state of the
`Http2Session`.

* Value: {Object}
  * `effectiveLocalWindowSize` {number} The current local (receive)
    flow control window size for the `Http2Session`.
  * `effectiveRecvDataLength` {number} The current number of bytes
    that have been received since the last flow control `WINDOW_UPDATE`.
  * `nextStreamID` {number} The numeric identifier to be used the
    next time a new `Http2Stream` is created by this `Http2Session`.
  * `localWindowSize` {number} The number of bytes that the remote peer can
    send without receiving a `WINDOW_UPDATE`.
  * `lastProcStreamID` {number} The numeric id of the `Http2Stream`
    for which a `HEADERS` or `DATA` frame was most recently received.
  * `remoteWindowSize` {number} The number of bytes that this `Http2Session`
    may send without receiving a `WINDOW_UPDATE`.
  * `outboundQueueSize` {number} The number of frames currently within the
    outbound queue for this `Http2Session`.
  * `deflateDynamicTableSize` {number} The current size in bytes of the
    outbound header compression state table.
  * `inflateDynamicTableSize` {number} The current size in bytes of the
    inbound header compression state table.

An object describing the current status of this `Http2Session`.

