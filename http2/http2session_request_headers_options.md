<!-- YAML
added: v8.4.0
-->

* `headers` {[Headers Object][]}
* `options` {Object}
  * `endStream` {boolean} `true` if the `Http2Stream` *writable* side should
    be closed initially, such as when sending a `GET` request that should not
    expect a payload body.
  * `exclusive` {boolean} When `true` and `parent` identifies a parent Stream,
    the created stream is made the sole direct dependency of the parent, with
    all other existing dependents made a dependent of the newly created stream.
    Defaults to `false`.
  * `parent` {number} Specifies the numeric identifier of a stream the newly
    created stream is dependent on.
  * `weight` {number} Specifies the relative dependency of a stream in relation
    to other streams with the same `parent`. The value is a number between `1`
    and `256` (inclusive).
  * `getTrailers` {Function} Callback function invoked to collect trailer
    headers.

* Returns: {ClientHttp2Stream}

For HTTP/2 Client `Http2Session` instances only, the `http2session.request()`
creates and returns an `Http2Stream` instance that can be used to send an
HTTP/2 request to the connected server.

This method is only available if `http2session.type` is equal to
`http2.constants.NGHTTP2_SESSION_CLIENT`.

```js
const http2 = require('http2');
const clientSession = http2.connect('https://localhost:1234');
const {
  HTTP2_HEADER_PATH,
  HTTP2_HEADER_STATUS
} = http2.constants;

const req = clientSession.request({ [HTTP2_HEADER_PATH]: '/' });
req.on('response', (headers) => {
  console.log(HTTP2_HEADER_STATUS);
  req.on('data', (chunk) => { /** .. **/ });
  req.on('end', () => { /** .. **/ });
});
```

When set, the `options.getTrailers()` function is called immediately after
queuing the last chunk of payload data to be sent. The callback is passed a
single object (with a `null` prototype) that the listener may used to specify
the trailing header fields to send to the peer.

*Note*: The HTTP/1 specification forbids trailers from containing HTTP/2
"pseudo-header" fields (e.g. `':method'`, `':path'`, etc). An `'error'` event
will be emitted if the `getTrailers` callback attempts to set such header
fields.

