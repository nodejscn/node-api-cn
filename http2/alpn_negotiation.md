
ALPN negotiation allows to support both [HTTPS][] and HTTP/2 over
the same socket. The `req` and `res` objects can be either HTTP/1 or
HTTP/2, and an application **must** restrict itself to the public API of
[HTTP/1][], and detect if it is possible to use the more advanced
features of HTTP/2.

The following example creates a server that supports both protocols:

```js
const { createSecureServer } = require('http2');
const { readFileSync } = require('fs');

const cert = fs.readFileSync('./cert.pem');
const key = fs.readFileSync('./key.pem');

const server = createSecureServer(
  { cert, key, allowHTTP1: true },
  onRequest
).listen(4443);

function onRequest(req, res) {
  // detects if it is a HTTPS request or HTTP/2
  const { socket: { alpnProtocol } } = request.httpVersion === '2.0' ?
    request.stream.session : request;
  response.writeHead(200, { 'content-type': 'application/json' });
  response.end(JSON.stringify({
    alpnProtocol,
    httpVersion: request.httpVersion
  }));
}
```

The `'request'` event works identically on both [HTTPS](https) and
HTTP/2.

