<!-- YAML
added: v8.4.0
-->

The `'response'` event is emitted when a response `HEADERS` frame has been
received for this stream from the connected HTTP/2 server. The listener is
invoked with two arguments: an Object containing the received
[Headers Object][], and flags associated with the headers.

For example:

```js
const http2 = require('http');
const client = http2.connect('https://localhost');
const req = client.request({ ':path': '/' });
req.on('response', (headers, flags) => {
  console.log(headers[':status']);
});
```

