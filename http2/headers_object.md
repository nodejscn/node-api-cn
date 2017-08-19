
Headers are represented as own-properties on JavaScript objects. The property
keys will be serialized to lower-case. Property values should be strings (if
they are not they will be coerced to strings) or an Array of strings (in order
to send more than one value per header field).

For example:

```js
const headers = {
  ':status': '200',
  'content-type': 'text-plain',
  'ABC': ['has', 'more', 'than', 'one', 'value']
};

stream.respond(headers);
```

*Note*: Header objects passed to callback functions will have a `null`
prototype. This means that normal JavaScript object methods such as
`Object.prototype.toString()` and `Object.prototype.hasOwnProperty()` will
not work.

```js
const http2 = require('http2');
const server = http2.createServer();
server.on('stream', (stream, headers) => {
  console.log(headers[':path']);
  console.log(headers.ABC);
});
```

