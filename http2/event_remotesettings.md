<!-- YAML
added: v8.4.0
-->

* `settings` {HTTP/2 Settings Object} A copy of the `SETTINGS` frame received.

The `'remoteSettings'` event is emitted when a new `SETTINGS` frame is received
from the connected peer.

```js
session.on('remoteSettings', (settings) => {
  /* Use the new settings */
});
```

