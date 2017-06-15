<!-- YAML
added: v0.7.0
-->

* {Object}

A hash that stores the active worker objects, keyed by `id` field. Makes it
easy to loop through all the workers. It is only available in the master
process.

A worker is removed from cluster.workers after the worker has disconnected _and_
exited. The order between these two events cannot be determined in advance.
However, it is guaranteed that the removal from the cluster.workers list happens
before last `'disconnect'` or `'exit'` event is emitted.

```js
// Go through all workers
function eachWorker(callback) {
  for (const id in cluster.workers) {
    callback(cluster.workers[id]);
  }
}
eachWorker((worker) => {
  worker.send('big announcement to all workers');
});
```

Using the worker's unique id is the easiest way to locate the worker.

```js
socket.on('data', (id) => {
  const worker = cluster.workers[id];
});
```

