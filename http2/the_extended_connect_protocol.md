
[RFC 8441][] defines an "Extended CONNECT Protocol" extension to HTTP/2 that
may be used to bootstrap the use of an `Http2Stream` using the `CONNECT`
method as a tunnel for other communication protocols (such as WebSockets).

The use of the Extended CONNECT Protocol is enabled by HTTP/2 servers by using
the `enableConnectProtocol` setting:

```js
const http2 = require('http2');
const settings = { enableConnectProtocol: true };
const server = http2.createServer({ settings });
```

Once the client receives the `SETTINGS` frame from the server indicating that
the extended CONNECT may be used, it may send `CONNECT` requests that use the
`':protocol'` HTTP/2 pseudo-header:

```js
const http2 = require('http2');
const client = http2.connect('http://localhost:8080');
client.on('remoteSettings', (settings) => {
  if (settings.enableConnectProtocol) {
    const req = client.request({ ':method': 'CONNECT', ':protocol': 'foo' });
    // ...
  }
});
```

