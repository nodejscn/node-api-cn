
On the server side, instances of [`ServerHttp2Stream`][] are created either
when:

* A new HTTP/2 `HEADERS` frame with a previously unused stream ID is received;
* The `http2stream.pushStream()` method is called.

On the client side, instances of [`ClientHttp2Stream`][] are created when the
`http2session.request()` method is called.

*Note*: On the client, the `Http2Stream` instance returned by
`http2session.request()` may not be immediately ready for use if the parent
`Http2Session` has not yet been fully established. In such cases, operations
called on the `Http2Stream` will be buffered until the `'ready'` event is
emitted. User code should rarely, if ever, have need to handle the `'ready'`
event directly. The ready status of an `Http2Stream` can be determined by
checking the value of `http2stream.id`. If the value is `undefined`, the stream
is not yet ready for use.

