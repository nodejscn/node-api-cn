<!-- YAML
added: v9.4.0
-->

* `alt`: {string}
* `origin`: {string}
* `streamId`: {number}

The `'altsvc'` event is emitted whenever an `ALTSVC` frame is received by
the client. The event is emitted with the `ALTSVC` value, origin, and stream
ID. If no `origin` is provided in the `ALTSVC` frame, `origin` will
be an empty string.

```js
const http2 = require('http2');
const client = http2.connect('https://example.org');

client.on('altsvc', (alt, origin, streamId) => {
  console.log(alt);
  console.log(origin);
  console.log(streamId);
});
```

