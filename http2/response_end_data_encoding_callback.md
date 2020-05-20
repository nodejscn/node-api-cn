<!-- YAML
added: v8.4.0
changes:
  - version: v10.0.0
    pr-url: https://github.com/nodejs/node/pull/18780
    description: This method now returns a reference to `ServerResponse`.
-->

* `data` {string|Buffer|Uint8Array}
* `encoding` {string}
* `callback` {Function}
* Returns: {this}

This method signals to the server that all of the response headers and body
have been sent; that server should consider this message complete.
The method, `response.end()`, MUST be called on each response.

If `data` is specified, it is equivalent to calling
[`response.write(data, encoding)`][] followed by `response.end(callback)`.

If `callback` is specified, it will be called when the response stream
is finished.

