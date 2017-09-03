
The Compatibility API has the goal of providing a similar developer experience
of HTTP/1 when using HTTP/2, making it possible to develop applications
that supports both [HTTP/1](HTTP/1) and HTTP/2. This API targets only the
**public API** of the [HTTP/1](HTTP/1), however many modules uses internal
methods or state, and those _are not supported_ as it is a completely
different implementation.

The following example creates an HTTP/2 server using the compatibility
API:

```js
const http2 = require('http2');
const server = http2.createServer((req, res) => {
  res.setHeader('Content-Type', 'text/html');
  res.setHeader('X-Foo', 'bar');
  res.writeHead(200, { 'Content-Type': 'text/plain' });
  res.end('ok');
});
```

In order to create a mixed [HTTPS][] and HTTP/2 server, refer to the
[ALPN negotiation][] section.
Upgrading from non-tls HTTP/1 servers is not supported.

The HTTP2 compatibility API is composed of [`Http2ServerRequest`]() and
[`Http2ServerResponse`](). They aim at API compatibility with HTTP/1, but
they do not hide the differences between the protocols. As an example,
the status message for HTTP codes is ignored.

