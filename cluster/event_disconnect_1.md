<!-- YAML
added: v0.7.9
-->

* `worker` {cluster.Worker}

Emitted after the worker IPC channel has disconnected. This can occur when a
worker exits gracefully, is killed, or is disconnected manually (such as with
worker.disconnect()).

There may be a delay between the `'disconnect'` and `'exit'` events.  These events
can be used to detect if the process is stuck in a cleanup or if there are
long-living connections.

```js
cluster.on('disconnect', (worker) => {
  console.log(`The worker #${worker.id} has disconnected`);
});
```

