
* `path` {string} 客户端要连接的路径。参见[识别 IPC 连接的路径][Identifying paths for IPC connections]。
* `connectListener` {Function} [`socket.connect()`] 方法的通用参数。将会作为 [`'connect'`] 事件的监听器被添加一次。
* 返回: {net.Socket} 套接字自身。


在给定的套接字上启动 [IPC] 连接。


使用 `{ path: path }` 作为 `options` 调用 [`socket.connect(options[, connectListener])`][`socket.connect(options)`] 的别名。


