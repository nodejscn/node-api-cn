<!-- YAML
added: v8.4.0
-->

* {net.Socket|tls.TLSSocket}

Returns a Proxy object that acts as a `net.Socket` (or `tls.TLSSocket`) but
applies getters, setters and methods based on HTTP/2 logic.

`destroyed`, `readable`, and `writable` properties will be retrieved from and
set on `response.stream`.

`destroy`, `emit`, `end`, `on` and `once` methods will be called on
`response.stream`.

`setTimeout` method will be called on `response.stream.session`.

`pause`, `read`, `resume`, and `write` will throw an error with code
`ERR_HTTP2_NO_SOCKET_MANIPULATION`. See [Http2Session and Sockets][] for
more information.

All other interactions will be routed directly to the socket.

Example:

```js
const http2 = require('http2');
const server = http2.createServer((req, res) => {
  const ip = req.socket.remoteAddress;
  const port = req.socket.remotePort;
  res.end(`Your IP address is ${ip} and your source port is ${port}.`);
}).listen(3000);
```

