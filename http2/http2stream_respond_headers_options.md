<!-- YAML
added: v8.4.0
-->

* `headers` {[Headers Object][]}
* `options` {Object}
  * `endStream` {boolean} Set to `true` to indicate that the response will not
    include payload data.
  * `getTrailers` {function} Callback function invoked to collect trailer
    headers.
* Returns: {undefined}

```js
const http2 = require('http2');
const server = http2.createServer();
server.on('stream', (stream) => {
  stream.respond({ ':status': 200 });
  stream.end('some data');
});
```

When set, the `options.getTrailers()` function is called immediately after
queuing the last chunk of payload data to be sent. The callback is passed a
single object (with a `null` prototype) that the listener may used to specify
the trailing header fields to send to the peer.

```js
const http2 = require('http2');
const server = http2.createServer();
server.on('stream', (stream) => {
  stream.respond({ ':status': 200 }, {
    getTrailers(trailers) {
      trailers['ABC'] = 'some value to send';
    }
  });
  stream.end('some data');
});
```

*Note*: The HTTP/1 specification forbids trailers from containing HTTP/2
"pseudo-header" fields (e.g. `':status'`, `':path'`, etc). An `'error'` event
will be emitted if the `getTrailers` callback attempts to set such header
fields.

