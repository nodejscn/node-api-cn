<!-- YAML
added: v0.2.0
deprecated: v0.9.7
-->

> 稳定性: 0 - 废弃的: 使用 [`server.getConnections()`] 代替。

服务器上现在同时存在的连接的数目.

当用[`child_process.fork()`][]向一个子进程发出socket连接时，这将变成`null`。
当poll新进程和获取活着的连接的数目时，可以用异步的`server.getConnections` 代替.

