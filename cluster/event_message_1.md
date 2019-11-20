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

当集群主进程从任何工作进程接收到消息时触发。

参阅 [`child_process` 事件 `'message'`][`child_process` event: `'message'`]。

