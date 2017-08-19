
All [`Http2Stream`][] instances are destroyed either when:

* An `RST_STREAM` frame for the stream is received by the connected peer.
* The `http2stream.rstStream()` or `http2session.rstStream()` methods are
  called.
* The `http2stream.destroy()` or `http2session.destroy()` methods are called.

When an `Http2Stream` instance is destroyed, an attempt will be made to send an
`RST_STREAM` frame will be sent to the connected peer.

Once the `Http2Stream` instance is destroyed, the `'streamClosed'` event will
be emitted. Because `Http2Stream` is an instance of `stream.Duplex`, the
`'end'` event will also be emitted if the stream data is currently flowing.
The `'error'` event may also be emitted if `http2stream.destroy()` was called
with an `Error` passed as the first argument.

After the `Http2Stream` has been destroyed, the `http2stream.destroyed`
property will be `true` and the `http2stream.rstCode` property will specify the
`RST_STREAM` error code. The `Http2Stream` instance is no longer usable once
destroyed.

