<!-- YAML
added: v0.7.0
changes:
  - version: v4.0.0
    pr-url: https://github.com/nodejs/node/pull/2620
    description: The `callback` parameter is supported now.
-->

* `message` {Object}
* `sendHandle` {Handle}
* `options` {Object} `options` 参数（如果存在）是一个对象，用于参数化某些类型的句柄的发送。`options` 支持以下属性：
  * `keepOpen` {boolean} 当传递 `net.Socket` 实例时可以使用的值。 当为 `true` 时，套接字在发送的过程中保持打开状态。**默认值:** `false`。
* `callback` {Function}
* 返回: {boolean}

发送消息给工作进程或主进程，可以选择带上句柄。

在主进程中，这会发送消息给特定的工作进程。
相当于 [`ChildProcess.send()`]。

在工作进程中，这会发送消息给主进程。
相当于 `process.send()`。

此示例将会回响主进程的所有消息：

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

