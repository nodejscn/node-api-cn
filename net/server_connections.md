<!-- YAML
added: v0.2.0
deprecated: v0.9.7
-->

> 稳定性: 0 - 废弃的: 使用 [`server.getConnections()`][] 来替代。

服务器上并发的连接数。

当发送一个 `socket` 给用`child_process.fork()` 创建的子进程时，这会返回 `null` 。要轮询分叉（forks）获得活动连接数可以使用异步的`server.getConnections()`来替代。
