<!-- YAML
added: v10.12.0
-->

* `origins` {string[]}

The `'origin'` event is emitted whenever an `ORIGIN` frame is received by
the client. The event is emitted with an array of `origin` strings. The
`http2session.originSet` will be updated to include the received
origins.

```js
const http2 = require('http2');
const client = http2.connect('https://example.org');

client.on('origin', (origins) => {
  for (let n = 0; n < origins.length; n++)
    console.log(origins[n]);
});
```

The `'origin'` event is only emitted when using a secure TLS connection.

