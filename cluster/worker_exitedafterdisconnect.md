<!-- YAML
added: v6.0.0
-->

* {Boolean}

Set by calling `.kill()` or `.disconnect()`. Until then, it is `undefined`.

The boolean `worker.exitedAfterDisconnect` lets you distinguish between voluntary
and accidental exit, the master may choose not to respawn a worker based on
this value.

```js
cluster.on('exit', (worker, code, signal) => {
  if (worker.exitedAfterDisconnect === true) {
    console.log('Oh, it was just voluntary – no need to worry');
  }
});

// kill worker
worker.kill();
```

