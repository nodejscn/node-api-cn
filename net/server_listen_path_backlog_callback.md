<!-- YAML
added: v0.1.90
-->

* `path` {string} 服务器需要监听的路径。查看 [识别 IPC 连接的路径。][Identifying paths for IPC connections]。
* `backlog` {number} [`server.listen()`] 函数的通用参数。
* `callback` {Function} [`server.listen()`] 函数的通用参数。
* 返回: {net.Server}

启动一个 [IPC] 服务器监听给定 `path` 的连接。
