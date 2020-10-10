<!-- YAML
added: v0.1.90
-->

* `port` {number} 客户端要连接的端口。
* `host` {string} 客户端要连接的主机。
* `connectListener` {Function} [`socket.connect()`] 方法的通用参数。将会作为 [`'connect'`] 事件的监听器被添加一次。
* 返回: {net.Socket} 套接字自身。


在给定的套接字上启动 TCP 连接。

使用 `{port: port, host: host}` 作为 `options` 调用 [`socket.connect(options[, connectListener])`][`socket.connect(options)`] 的别名。

