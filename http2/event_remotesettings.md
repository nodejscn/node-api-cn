<!-- YAML
added: v8.4.0
-->

The `'remoteSettings'` event is emitted when a new SETTINGS frame is received
from the connected peer. When invoked, the handle function will receive a copy
of the remote settings.

```js
session.on('remoteSettings', (settings) => {
  /** use the new settings **/
});
```

