<!-- YAML
added: v0.1.90
changes:
  - version: v0.11.6
    description: add `callback` argument.
-->

* `chunk` {string | Buffer}
* `encoding` {string} Optional, **Default**: `utf8`
* `callback` {Function} Optional
* Returns: {this}

Finishes the outgoing message. If any parts of the body are unsent, it will
flush them to the underlying system. If the message is chunked, it will
send the terminating chunk `0\r\n\r\n`, and send the trailer (if any).

If `chunk` is specified, it is equivalent to call
`outgoingMessage.write(chunk, encoding)`, followed by
`outgoingMessage.end(callback)`.

If `callback` is provided, it will be called when the message is finished.
(equivalent to the callback to event `finish`)

