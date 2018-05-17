<!-- YAML
added: v9.4.0
-->

* `callback` {Function}

Gracefully closes the `Http2Session`, allowing any existing streams to
complete on their own and preventing new `Http2Stream` instances from being
created. Once closed, `http2session.destroy()` *might* be called if there
are no open `Http2Stream` instances.

If specified, the `callback` function is registered as a handler for the
`'close'` event.

