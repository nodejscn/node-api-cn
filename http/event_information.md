<!-- YAML
added: v10.0.0
-->

Emitted when the server sends a 1xx response (excluding 101 Upgrade). This
event is emitted with a callback containing an object with a status code.

```js
const http = require('http');

const options = {
  hostname: '127.0.0.1',
  port: 8080,
  path: '/length_request'
};

// Make a request
const req = http.request(options);
req.end();

req.on('information', (res) => {
  console.log(`Got information prior to main response: ${res.statusCode}`);
});
```

101 Upgrade statuses do not fire this event due to their break from the
traditional HTTP request/response chain, such as web sockets, in-place TLS
upgrades, or HTTP 2.0. To be notified of 101 Upgrade notices, listen for the
[`'upgrade'`][] event instead.

