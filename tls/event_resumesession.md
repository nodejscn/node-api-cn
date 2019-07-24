<!-- YAML
added: v0.9.2
-->

The `'resumeSession'` event is emitted when the client requests to resume a
previous TLS session. The listener callback is passed two arguments when
called:

* `sessionId` {Buffer} The TLS session identifier
* `callback` {Function} A callback function to be called when the prior session
  has been recovered: `callback([err[, sessionData]])`
  * `err` {Error}
  * `sessionData` {Buffer}

The event listener should perform a lookup in external storage for the
`sessionData` saved by the [`'newSession'`][] event handler using the given
`sessionId`. If found, call `callback(null, sessionData)` to resume the session.
If not found, the session cannot be resumed. `callback()` must be called
without `sessionData` so that the handshake can continue and a new session can
be created. It is possible to call `callback(err)` to terminate the incoming
connection and destroy the socket.

Listening for this event will have an effect only on connections established
after the addition of the event listener.

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

