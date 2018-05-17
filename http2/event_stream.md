<!-- YAML
added: v8.4.0
-->

* `stream` {Http2Stream} A reference to the stream
* `headers` {HTTP/2 Headers Object} An object describing the headers
* `flags` {number} The associated numeric flags
* `rawHeaders` {Array} An array containing the raw header names followed by
  their respective values.

The `'stream'` event is emitted when a new `Http2Stream` is created.

```js
const http2 = require('http2');
session.on('stream', (stream, headers, flags) => {
  const method = headers[':method'];
  const path = headers[':path'];
  // ...
  stream.respond({
    ':status': 200,
    'content-type': 'text/plain'
  });
  stream.write('hello ');
  stream.end('world');
});
```

On the server side, user code will typically not listen for this event directly,
and would instead register a handler for the `'stream'` event emitted by the
`net.Server` or `tls.Server` instances returned by `http2.createServer()` and
`http2.createSecureServer()`, respectively, as in the example below:

```js
const http2 = require('http2');

// Create an unencrypted HTTP/2 server
const server = http2.createServer();

server.on('stream', (stream, headers) => {
  stream.respond({
    'content-type': 'text/html',
    ':status': 200
  });
  stream.end('<h1>Hello World</h1>');
});

server.listen(80);
```

