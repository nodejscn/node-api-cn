<!-- YAML
added: v0.1.90
-->

* `port` {number} 客户端连接的端口。
* `host` {string} 客户端连接的主机。
* `connectListener` {Function} [`socket.connect()`][] 方法的通用参数。将会被添加为 [`'connect'`][] 事件的监听器。
* Returns: {net.Socket} Socket 本身。

在给定的 socket 上初始化一个 TCP 连接。

使用 `{port: port, host: host}` 作为 `options` 调用 [`socket.connect(options[, connectListener])`][`socket.connect(options)`] 方法的别名。

返回 `socket`。

