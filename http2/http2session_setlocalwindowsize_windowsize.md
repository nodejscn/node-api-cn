<!-- YAML
added: v15.3.0
-->

* `windowSize` {number}

Sets the local endpoint's window size.
The `windowSize` is the total window size to set, not
the delta.

```js
const http2 = require('http2');

const server = http2.createServer();
const expectedWindowSize = 2 ** 20;
server.on('connect', (session) => {

  // Set local window size to be 2 ** 20
  session.setLocalWindowSize(expectedWindowSize);
});
```

