<!-- YAML
added: v0.9.4
-->

* `chunk` {String|Buffer} The data to write
* `encoding` {String} The encoding, if `chunk` is a String
* `callback` {Function} Callback for when this chunk of data is flushed
* Returns: {Boolean} `false` if the stream wishes for the calling code to
  wait for the `'drain'` event to be emitted before continuing to write
  additional data; otherwise `true`.

The `writable.write()` method writes some data to the stream, and calls the
supplied `callback` once the data has been fully handled. If an error
occurs, the `callback` *may or may not* be called with the error as its
first argument. To reliably detect write errors, add a listener for the
`'error'` event.

The return value is `true` if the internal buffer does not exceed
`highWaterMark` configured when the stream was created after admitting `chunk`.
If `false` is returned, further attempts to write data to the stream should
stop until the [`'drain'`][] event is emitted. However, the `false` return
value is only advisory and the writable stream will unconditionally accept and
buffer `chunk` even if it has not not been allowed to drain.

A Writable stream in object mode will always ignore the `encoding` argument.

