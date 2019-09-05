<!-- YAML
added: v0.7.2
-->

* {boolean}

如果 Node.js 进程是由 IPC 通道（参阅[子进程][Child Process]和[集群][Cluster]的文档）的方式创建，则只要 IPC 通道保持连接，`process.connected` 属性就会返回 `true`。
`process.disconnect()` 被调用后，此属性会返回 `false`。

一旦 `process.connected` 为 `false`，则不能通过 IPC 通道使用 `process.send()` 发送信息。


