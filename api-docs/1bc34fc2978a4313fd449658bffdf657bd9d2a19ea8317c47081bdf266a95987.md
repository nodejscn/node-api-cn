<!-- YAML
added: v2.5.0
changes:
  - version: v6.0.0
    pr-url: https://github.com/nodejs/node/pull/5361
    description: The `worker` parameter is passed now; see below for details.
-->

* `worker` {cluster.Worker}
* `message` {Object}
* `handle` {undefined|Object}

当 cluster 主进程接收任意工作进程发送的消息时触发。

参阅 [`child_process` event: `'message'`]。

在 Node.js v6.0 版本之前，此事件只接受 `message` 和 `handle` 两个参数，而没有 `worker` 对象。

如果要兼容旧版本并且不需要工作进程对象的情况下，可以通过判断参数数量来实现兼容。

```js
cluster.on('message', (worker, message, handle) => {
  if (arguments.length === 2) {
    handle = message;
    message = worker;
    worker = undefined;
  }
  // ...
});
```

