<!-- YAML
added: v0.1.90
-->

* `path` {String} 服务器需要监听的路径。查看 [Identifying paths for IPC connections][]。
* `backlog` {number} [`server.listen()`][] 通用参数。
* `callback` {Function} [`server.listen()`][] 通用参数。
* Returns: {net.Server}

启动一个 [IPC][] 服务器监听给定 `path` 的连接。
