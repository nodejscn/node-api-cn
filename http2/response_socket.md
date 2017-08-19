<!-- YAML
added: v8.4.0
-->

* {net.Socket}

Reference to the underlying socket. Usually users will not want to access
this property. In particular, the socket will not emit `'readable'` events
because of how the protocol parser attaches to the socket. After
`response.end()`, the property is nulled. The `socket` may also be accessed
via `response.connection`.

Example:

```js
const http2 = require('http2');
const server = http2.createServer((req, res) => {
  const ip = req.socket.remoteAddress;
  const port = req.socket.remotePort;
  res.end(`Your IP address is ${ip} and your source port is ${port}.`);
}).listen(3000);
```

