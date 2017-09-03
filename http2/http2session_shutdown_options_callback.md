<!-- YAML
added: v8.4.0
-->

* `options` {Object}
  * `graceful` {boolean} `true` to attempt a polite shutdown of the
    `Http2Session`.
  * `errorCode` {number} The HTTP/2 [error code][] to return. Note that this is
    *not* the same thing as an HTTP Response Status Code. Defaults to `0x00`
    (No Error).
  * `lastStreamID` {number} The Stream ID of the last successfully processed
    `Http2Stream` on this `Http2Session`.
  * `opaqueData` {Buffer|Uint8Array} A `Buffer` or `Uint8Array` instance
    containing arbitrary additional data to send to the peer upon disconnection.
    This is used, typically, to provide additional data for debugging failures,
    if necessary.
* `callback` {Function} A callback that is invoked after the session shutdown
  has been completed.
* Returns: {undefined}

Attempts to shutdown this `Http2Session` using HTTP/2 defined procedures.
If specified, the given `callback` function will be invoked once the shutdown
process has completed.

Note that calling `http2session.shutdown()` does *not* destroy the session or
tear down the `Socket` connection. It merely prompts both sessions to begin
preparing to cease activity.

During a "graceful" shutdown, the session will first send a `GOAWAY` frame to
the connected peer identifying the last processed stream as 2<sup>32</sup>-1.
Then, on the next tick of the event loop, a second `GOAWAY` frame identifying
the most recently processed stream identifier is sent. This process allows the
remote peer to begin preparing for the connection to be terminated.

```js
session.shutdown({
  graceful: true,
  opaqueData: Buffer.from('add some debugging data here')
}, () => session.destroy());
```

