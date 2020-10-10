<!-- YAML
added: v10.0.0
-->

* `headers` {HTTP/2 Headers Object}

Sends a trailing `HEADERS` frame to the connected HTTP/2 peer. This method
will cause the `Http2Stream` to be immediately closed and must only be
called after the `'wantTrailers'` event has been emitted. When sending a
request or sending a response, the `options.waitForTrailers` option must be set
in order to keep the `Http2Stream` open after the final `DATA` frame so that
trailers can be sent.

```js
const http2 = require('http2');
const server = http2.createServer();
server.on('stream', (stream) => {
  stream.respond(undefined, { waitForTrailers: true });
  stream.on('wantTrailers', () => {
    stream.sendTrailers({ xyz: 'abc' });
  });
  stream.end('Hello World');
});
```

The HTTP/1 specification forbids trailers from containing HTTP/2 pseudo-header
fields (e.g. `':method'`, `':path'`, etc).

