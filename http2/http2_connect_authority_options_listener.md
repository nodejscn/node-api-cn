<!-- YAML
added: v8.4.0
changes:
  - version: v8.9.3
    pr-url: https://github.com/nodejs/node/pull/17105
    description: Added the `maxOutstandingPings` option with a default limit of
                 10.
  - version: v8.9.3
    pr-url: https://github.com/nodejs/node/pull/16676
    description: Added the `maxHeaderListPairs` option with a default limit of
                 128 header pairs.
-->

* `authority` {string|URL}
* `options` {Object}
  * `maxDeflateDynamicTableSize` {number} Sets the maximum dynamic table size
    for deflating header fields. **Default:** `4Kib`
  * `maxHeaderListPairs` {number} Sets the maximum number of header entries.
    **Default:** `128`. The minimum value is `1`.
  * `maxOutstandingPings` {number} Sets the maximum number of outstanding,
    unacknowledged pings. The default is `10`.
  * `maxReservedRemoteStreams` {number} Sets the maximum number of reserved push
    streams the client will accept at any given time. Once the current number of
    currently reserved push streams exceeds reaches this limit, new push streams
    sent by the server will be automatically rejected.
  * `maxSendHeaderBlockLength` {number} Sets the maximum allowed size for a
    serialized, compressed block of headers. Attempts to send headers that
    exceed this limit will result in a `'frameError'` event being emitted
    and the stream being closed and destroyed.
  * `paddingStrategy` {number} Identifies the strategy used for determining the
     amount of padding to use for HEADERS and DATA frames. **Default:**
     `http2.constants.PADDING_STRATEGY_NONE`. Value may be one of:
     * `http2.constants.PADDING_STRATEGY_NONE` - Specifies that no padding is
       to be applied.
     * `http2.constants.PADDING_STRATEGY_MAX` - Specifies that the maximum
       amount of padding, as determined by the internal implementation, is to
       be applied.
     * `http2.constants.PADDING_STRATEGY_CALLBACK` - Specifies that the user
       provided `options.selectPadding` callback is to be used to determine the
       amount of padding.
  * `peerMaxConcurrentStreams` {number} Sets the maximum number of concurrent
    streams for the remote peer as if a SETTINGS frame had been received. Will
    be overridden if the remote peer sets its own value for
    `maxConcurrentStreams`. **Default:** `100`
  * `selectPadding` {Function} When `options.paddingStrategy` is equal to
    `http2.constants.PADDING_STRATEGY_CALLBACK`, provides the callback function
    used to determine the padding. See [Using options.selectPadding][].
  * `settings` {[Settings Object][]} The initial settings to send to the
    remote peer upon connection.
  * `createConnection` {Function} An optional callback that receives the `URL`
    instance passed to `connect` and the `options` object, and returns any
    [`Duplex`][] stream that is to be used as the connection for this session.
  * ...: Any [`net.connect()`][] or [`tls.connect()`][] options can be provided.
* `listener` {Function}
* Returns {Http2Session}

Returns a HTTP/2 client `Http2Session` instance.

```js
const http2 = require('http2');
const client = http2.connect('https://localhost:1234');

/** use the client **/

client.destroy();
```

