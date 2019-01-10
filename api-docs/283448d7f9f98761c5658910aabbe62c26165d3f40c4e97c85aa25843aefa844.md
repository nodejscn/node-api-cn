<!-- YAML
added: v8.4.0
-->

* `error` {Error} An `Error` object if the `Http2Session` is being destroyed
  due to an error.
* `code` {number} The HTTP/2 error code to send in the final `GOAWAY` frame.
  If unspecified, and `error` is not undefined, the default is `INTERNAL_ERROR`,
  otherwise defaults to `NO_ERROR`.

Immediately terminates the `Http2Session` and the associated `net.Socket` or
`tls.TLSSocket`.

Once destroyed, the `Http2Session` will emit the `'close'` event. If `error`
is not undefined, an `'error'` event will be emitted immediately before the
`'close'` event.

If there are any remaining open `Http2Streams` associated with the
`Http2Session`, those will also be destroyed.

