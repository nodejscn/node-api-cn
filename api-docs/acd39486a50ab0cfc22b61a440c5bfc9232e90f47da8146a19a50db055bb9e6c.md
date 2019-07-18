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
* 返回: {boolean}

发送一个消息给工作进程或主进程，也可以附带发送一个句柄。

在主进程中，这会发送消息给特定的工作进程。
相当于 [`ChildProcess.send()`]。

在工作进程中，这会发送消息给主进程。
相当于 `process.send()`。

这个例子里面，工作进程将主进程发送的消息响应回去：

```js
if (cluster.isMaster) {
  const worker = cluster.fork();
  worker.send('你好');

} else if (cluster.isWorker) {
  process.on('message', (msg) => {
    process.send(msg);
  });
}
```

