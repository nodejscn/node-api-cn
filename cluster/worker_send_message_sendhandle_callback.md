<!-- YAML
added: v0.7.0
-->

* `message` {Object}
* `sendHandle` {Handle}
* `callback` {Function}
* Returns: Boolean

Send a message to a worker or master, optionally with a handle.

In the master this sends a message to a specific worker. It is identical to
[`ChildProcess.send()`][].

In a worker this sends a message to the master. It is identical to
`process.send()`.

This example will echo back all messages from the master:

```js
if (cluster.isMaster) {
  var worker = cluster.fork();
  worker.send('hi there');

} else if (cluster.isWorker) {
  process.on('message', (msg) => {
    process.send(msg);
  });
}
```

