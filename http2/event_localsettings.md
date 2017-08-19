<!-- YAML
added: v8.4.0
-->

The `'localSettings'` event is emitted when an acknowledgement SETTINGS frame
has been received. When invoked, the handler function will receive a copy of
the local settings.

*Note*: When using `http2session.settings()` to submit new settings, the
modified settings do not take effect until the `'localSettings'` event is
emitted.

```js
session.settings({ enablePush: false });

session.on('localSettings', (settings) => {
  /** use the new settings **/
});
```

