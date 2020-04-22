<!-- YAML
added: v13.7.0
-->

* `err` {Error} The uncaught exception.
* `origin` {string} Indicates if the exception originates from an unhandled
  rejection or from synchronous errors. Can either be `'uncaughtException'` or
  `'unhandledRejection'`.

The `'uncaughtExceptionMonitor'` event is emitted before an
`'uncaughtException'` event is emitted or a hook installed via
[`process.setUncaughtExceptionCaptureCallback()`][] is called.

Installing an `'uncaughtExceptionMonitor'` listener does not change the behavior
once an `'uncaughtException'` event is emitted. The process will
still crash if no `'uncaughtException'` listener is installed.

```js
process.on('uncaughtExceptionMonitor', (err, origin) => {
  MyMonitoringTool.logSync(err, origin);
});

// Intentionally cause an exception, but don't catch it.
nonexistentFunc();
// Still crashes Node.js
```

