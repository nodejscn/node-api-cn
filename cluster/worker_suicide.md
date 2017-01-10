<!-- YAML
added: v0.7.0
deprecated: v6.0.0
-->

> Stability: 0 - Deprecated: Use [`worker.exitedAfterDisconnect`][] instead.

An alias to [`worker.exitedAfterDisconnect`][].

Set by calling `.kill()` or `.disconnect()`. Until then, it is `undefined`.

The boolean `worker.suicide` lets you distinguish between voluntary
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

