
* `path` {string} 客户端连接的路径. 查看 [Identifying paths for IPC connections][]。
* `connectListener` {Function} [`socket.connect()`][] 方法的通用参数。将被添加为 [`'connect'`][] 事件的监听器。
* Returns: {net.Socket} Socket 自身。

在给定的 socket 上初始化 [IPC][] 。

相当使用 `{ path: path }` 作为 `options` 调用 [`socket.connect(options[, connectListener])`][`socket.connect(options)`] 方法的别名。

返回 `socket`。

