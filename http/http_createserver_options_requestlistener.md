<!-- YAML
added: v0.1.13
changes:
  - version: v9.6.0
    pr-url: https://github.com/nodejs/node/pull/15752
    description: The `options` argument is supported now.
-->
- `options` {Object}
  * `IncomingMessage` {http.IncomingMessage} Specifies the `IncomingMessage`
    class to be used. Useful for extending the original `IncomingMessage`.
    **Default:** `IncomingMessage`.
  * `ServerResponse` {http.ServerResponse} Specifies the `ServerResponse` class
    to be used. Useful for extending the original `ServerResponse`. **Default:**
    `ServerResponse`.
- `requestListener` {Function}

* Returns: {http.Server}

Returns a new instance of [`http.Server`][].

The `requestListener` is a function which is automatically
added to the [`'request'`][] event.

