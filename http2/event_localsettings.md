<!-- YAML
added: v8.4.0
-->

* `settings` {HTTP/2 Settings Object} A copy of the `SETTINGS` frame received.

The `'localSettings'` event is emitted when an acknowledgment `SETTINGS` frame
has been received.

When using `http2session.settings()` to submit new settings, the modified
settings do not take effect until the `'localSettings'` event is emitted.

```js
session.settings({ enablePush: false });

session.on('localSettings', (settings) => {
  /* Use the new settings */
});
```

