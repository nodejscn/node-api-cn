<!-- YAML
added: v8.4.0
-->

* `headers` {[Headers Object][]}
* `options` {Object}
  * `exclusive` {boolean} When `true` and `parent` identifies a parent Stream,
    the created stream is made the sole direct dependency of the parent, with
    all other existing dependents made a dependent of the newly created stream.
    **Default:** `false`
  * `parent` {number} Specifies the numeric identifier of a stream the newly
    created stream is dependent on.
* `callback` {Function} Callback that is called once the push stream has been
  initiated.
* Returns: {undefined}

Initiates a push stream. The callback is invoked with the new `Http2Stream`
instance created for the push stream.

```js
const http2 = require('http2');
const server = http2.createServer();
server.on('stream', (stream) => {
  stream.respond({ ':status': 200 });
  stream.pushStream({ ':path': '/' }, (pushStream) => {
    pushStream.respond({ ':status': 200 });
    pushStream.end('some pushed data');
  });
  stream.end('some data');
});
```

Setting the weight of a push stream is not allowed in the `HEADERS` frame. Pass
a `weight` value to `http2stream.priority` with the `silent` option set to
`true` to enable server-side bandwidth balancing between concurrent streams.

