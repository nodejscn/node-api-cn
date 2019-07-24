<!-- YAML
added: v0.7.2
-->

* {boolean}

如果Node.js进程是由IPC channel方式创建的(请看[Child Process子进程][] 和 [Cluster集群][] 文档)，
只要IPC channel保持连接，`process.connected`属性就会返回`true`。
`process.disconnect()`被调用后，此属性会返回`false`。

`process.connected`如果为`false`，则不能通过IPC channel使用`process.send()`发送信息。


