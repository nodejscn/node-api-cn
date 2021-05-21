<!-- YAML
added: v8.4.0
changes:
  - version:
      - v15.10.0
      - v14.16.0
      - v12.21.0
      - v10.24.0
    pr-url: https://github.com/nodejs-private/node-private/pull/246
    description: Added `unknownProtocolTimeout` option with a default of 10000.
  - version:
     - v14.4.0
     - v12.18.0
     - v10.21.0
    commit: 3948830ce6408be620b09a70bf66158623022af0
    pr-url: https://github.com/nodejs-private/node-private/pull/204
    description: Added `maxSettings` option with a default of 32.
  - version:
     - v13.3.0
     - v12.16.0
    pr-url: https://github.com/nodejs/node/pull/30534
    description: Added `maxSessionRejectedStreams` option with a default of 100.
  - version:
     - v13.3.0
     - v12.16.0
    pr-url: https://github.com/nodejs/node/pull/30534
    description: Added `maxSessionInvalidFrames` option with a default of 1000.
  - version: v13.0.0
    pr-url: https://github.com/nodejs/node/pull/29144
    description: The `PADDING_STRATEGY_CALLBACK` has been made equivalent to
                 providing `PADDING_STRATEGY_ALIGNED` and `selectPadding`
                 has been removed.
  - version: v12.4.0
    pr-url: https://github.com/nodejs/node/pull/27782
    description: The `options` parameter now supports `net.createServer()`
                 options.
  - version: v9.6.0
    pr-url: https://github.com/nodejs/node/pull/15752
    description: Added the `Http1IncomingMessage` and `Http1ServerResponse`
                 option.
  - version: v8.9.3
    pr-url: https://github.com/nodejs/node/pull/17105
    description: Added the `maxOutstandingPings` option with a default limit of
                 10.
  - version: v8.9.3
    pr-url: https://github.com/nodejs/node/pull/16676
    description: Added the `maxHeaderListPairs` option with a default limit of
                 128 header pairs.
-->

* `options` {Object}
  * `maxDeflateDynamicTableSize` {number} Sets the maximum dynamic table size
    for deflating header fields. **Default:** `4Kib`.
  * `maxSettings` {number} Sets the maximum number of settings entries per
    `SETTINGS` frame. The minimum value allowed is `1`. **Default:** `32`.
  * `maxSessionMemory`{number} Sets the maximum memory that the `Http2Session`
    is permitted to use. The value is expressed in terms of number of megabytes,
    e.g. `1` equal 1 megabyte. The minimum value allowed is `1`.
    This is a credit based limit, existing `Http2Stream`s may cause this
    limit to be exceeded, but new `Http2Stream` instances will be rejected
    while this limit is exceeded. The current number of `Http2Stream` sessions,
    the current memory use of the header compression tables, current data
    queued to be sent, and unacknowledged `PING` and `SETTINGS` frames are all
    counted towards the current limit. **Default:** `10`.
  * `maxHeaderListPairs` {number} Sets the maximum number of header entries.
    This is similar to [`http.Server#maxHeadersCount`][] or
    [`http.ClientRequest#maxHeadersCount`][]. The minimum value is `4`.
    **Default:** `128`.
  * `maxOutstandingPings` {number} Sets the maximum number of outstanding,
    unacknowledged pings. **Default:** `10`.
  * `maxSendHeaderBlockLength` {number} Sets the maximum allowed size for a
    serialized, compressed block of headers. Attempts to send headers that
    exceed this limit will result in a `'frameError'` event being emitted
    and the stream being closed and destroyed.
  * `paddingStrategy` {number} The strategy used for determining the amount of
    padding to use for `HEADERS` and `DATA` frames. **Default:**
    `http2.constants.PADDING_STRATEGY_NONE`. Value may be one of:
    * `http2.constants.PADDING_STRATEGY_NONE`: No padding is applied.
    * `http2.constants.PADDING_STRATEGY_MAX`: The maximum amount of padding,
      determined by the internal implementation, is applied.
    * `http2.constants.PADDING_STRATEGY_ALIGNED`: Attempts to apply enough
      padding to ensure that the total frame length, including the 9-byte
      header, is a multiple of 8. For each frame, there is a maximum allowed
      number of padding bytes that is determined by current flow control state
      and settings. If this maximum is less than the calculated amount needed to
      ensure alignment, the maximum is used and the total frame length is not
      necessarily aligned at 8 bytes.
  * `peerMaxConcurrentStreams` {number} Sets the maximum number of concurrent
    streams for the remote peer as if a `SETTINGS` frame had been received. Will
    be overridden if the remote peer sets its own value for
    `maxConcurrentStreams`. **Default:** `100`.
  * `maxSessionInvalidFrames` {integer} Sets the maximum number of invalid
    frames that will be tolerated before the session is closed.
    **Default:** `1000`.
  * `maxSessionRejectedStreams` {integer} Sets the maximum number of rejected
    upon creation streams that will be tolerated before the session is closed.
    Each rejection is associated with an `NGHTTP2_ENHANCE_YOUR_CALM`
    error that should tell the peer to not open any more streams, continuing
    to open streams is therefore regarded as a sign of a misbehaving peer.
    **Default:** `100`.
  * `settings` {HTTP/2 Settings Object} The initial settings to send to the
    remote peer upon connection.
  * `Http1IncomingMessage` {http.IncomingMessage} Specifies the
    `IncomingMessage` class to used for HTTP/1 fallback. Useful for extending
    the original `http.IncomingMessage`. **Default:** `http.IncomingMessage`.
  * `Http1ServerResponse` {http.ServerResponse} Specifies the `ServerResponse`
    class to used for HTTP/1 fallback. Useful for extending the original
    `http.ServerResponse`. **Default:** `http.ServerResponse`.
  * `Http2ServerRequest` {http2.Http2ServerRequest} Specifies the
    `Http2ServerRequest` class to use.
    Useful for extending the original `Http2ServerRequest`.
    **Default:** `Http2ServerRequest`.
  * `Http2ServerResponse` {http2.Http2ServerResponse} Specifies the
    `Http2ServerResponse` class to use.
    Useful for extending the original `Http2ServerResponse`.
    **Default:** `Http2ServerResponse`.
  * `unknownProtocolTimeout` {number} Specifies a timeout in milliseconds that
    a server should wait when an [`'unknownProtocol'`][] is emitted. If the
    socket has not been destroyed by that time the server will destroy it.
    **Default:** `10000`.
  * ...: Any [`net.createServer()`][] option can be provided.
* `onRequestHandler` {Function} See [Compatibility API][]
* Returns: {Http2Server}

Returns a `net.Server` instance that creates and manages `Http2Session`
instances.

Since there are no browsers known that support
[unencrypted HTTP/2][HTTP/2 Unencrypted], the use of
[`http2.createSecureServer()`][] is necessary when communicating
with browser clients.

```js
const http2 = require('http2');

// Create an unencrypted HTTP/2 server.
// Since there are no browsers known that support
// unencrypted HTTP/2, the use of `http2.createSecureServer()`
// is necessary when communicating with browser clients.
const server = http2.createServer();

server.on('stream', (stream, headers) => {
  stream.respond({
    'content-type': 'text/html; charset=utf-8',
    ':status': 200
  });
  stream.end('<h1>Hello World</h1>');
});

server.listen(80);
```

