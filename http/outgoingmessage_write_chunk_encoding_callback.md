<!-- YAML
added: v0.1.29
changes:
  - version: v0.11.6
    description: add `callback` argument.
-->

* `chunk` {string | Buffer}
* `encoding` {string} **Default**: `utf8`
* `callback` {Function}
* Returns {boolean}

If this method is called and the header is not sent, it will call
`this._implicitHeader` to flush implicit header.
If the message should not have a body (indicated by `this._hasBody`),
the call is ignored and `chunk` will not be sent. It could be useful
when handling a particular message which must not include a body.
e.g. response to `HEAD` request, `204` and `304` response.

`chunk` can be a string or a buffer. When `chunk` is a string, the
`encoding` parameter specifies how to encode `chunk` into a byte stream.
`callback` will be called when the `chunk` is flushed.

If the message is transferred in chucked encoding
(indicated by `this.chunkedEncoding`), `chunk` will be flushed as
one chunk among a stream of chunks. Otherwise, it will be flushed as the
body of message.

This method handles the raw body of the HTTP message and has nothing to do
with higher-level multi-part body encodings that may be used.

If it is the first call to this method of a message, it will send the
buffered header first, then flush the `chunk` as described above.

The second and successive calls to this method will assume the data
will be streamed and send the new data separately. It means that the response
is buffered up to the first chunk of the body.

Returns `true` if the entire data was flushed successfully to the kernel
buffer. Returns `false` if all or part of the data was queued in the user
memory. Event `drain` will be emitted when the buffer is free again.

