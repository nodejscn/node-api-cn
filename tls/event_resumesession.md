<!-- YAML
added: v0.9.2
-->

The `'resumeSession'` event is emitted when the client requests to resume a
previous TLS session. The listener callback is passed two arguments when
called:

* `sessionId` - The TLS/SSL session identifier
* `callback` {Function} A callback function to be called when the prior session
  has been recovered.

When called, the event listener may perform a lookup in external storage using
the given `sessionId` and invoke `callback(null, sessionData)` once finished. If
the session cannot be resumed (i.e., doesn't exist in storage) the callback may
be invoked as `callback(null, null)`. Calling `callback(err)` will terminate the
incoming connection and destroy the socket.

*Note*: Listening for this event will have an effect only on connections
established after the addition of the event listener.

The following illustrates resuming a TLS session:

```js
const tlsSessionStore = {};
server.on('newSession', (id, data, cb) => {
  tlsSessionStore[id.toString('hex')] = data;
  cb();
});
server.on('resumeSession', (id, cb) => {
  cb(null, tlsSessionStore[id.toString('hex')] || null);
});
```

