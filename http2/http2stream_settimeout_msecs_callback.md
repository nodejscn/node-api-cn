<!-- YAML
added: v8.4.0
-->

* `msecs` {number}
* `callback` {Function}
* Returns: {undefined}

```js
const http2 = require('http2');
const client = http2.connect('http://example.org:8000');

const req = client.request({ ':path': '/' });

// Cancel the stream if there's no activity after 5 seconds
req.setTimeout(5000, () => req.rstStreamWithCancel());
```

