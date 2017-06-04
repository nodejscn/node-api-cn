<!-- YAML
added: v0.7.0
deprecated: v6.0.0
changes:
  - version: v7.0.0
    pr-url: https://github.com/nodejs/node/pull/3747
    description: Accessing this property will now emit a deprecation warning.
-->

> Stability: 0 - Deprecated: Use [`worker.exitedAfterDisconnect`][] instead.

An alias to [`worker.exitedAfterDisconnect`][].

Set by calling `.kill()` or `.disconnect()`. Until then, it is `undefined`.

The boolean `worker.suicide` is used to distinguish between voluntary
and accidental exit, the master may choose not to respawn a worker based on
this value.

```js
cluster.on('exit', (worker, code, signal) => {
  if (worker.suicide === true) {
    console.log('Oh, it was just voluntary – no need to worry');
  }
});

// kill worker
worker.kill();
```

This API only exists for backwards compatibility and will be removed in the
future.

