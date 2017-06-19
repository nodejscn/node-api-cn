<!-- YAML
added: v0.7.0
changes:
  - version: v4.0.0
    pr-url: https://github.com/nodejs/node/pull/2620
    description: The `callback` parameter is supported now.
-->

* `message` {Object}
* `sendHandle` {Handle}
* `callback` {Function}
* Returns: Boolean

发送一个消息给工作进程或主进程，也可以附带发送一个handle。

主进程调用这个方法会发送消息给具体的工作进程。还有一个等价的方法是[`ChildProcess.send()`][]。

工作进程调用这个方法会发送消息给主进程。还有一个等价方法是`process.send()`。

这个例子里面，工作进程将主进程发送的消息echo回去。

```js
if (cluster.isMaster) {
  const worker = cluster.fork();
  worker.send('hi there');

} else if (cluster.isWorker) {
  process.on('message', (msg) => {
    process.send(msg);
  });
}
```

