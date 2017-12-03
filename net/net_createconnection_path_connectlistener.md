<!-- YAML
added: v0.1.90
-->

* `path` {string} Socket 应该被连接到的路径。将会被传入到 [`socket.connect(path[, connectListener])`][`socket.connect(path)`]。查看 [Identifying paths for IPC connections][]。
* `connectListener` {Function} [`net.createConnection()`][] 方法的通用参数，在初始化的 socket 上的 `'connect'` 事件的 "once" 监听器。将会被传入到 [`socket.connect(path[, connectListener])`][`socket.connect(path)`]。
* Returns: {net.Socket} 新创建的 socket，用来开始连接。

初始化一个 [IPC][] 连接。

该方法使用所有默认选项创建一个新的 [`net.Socket`][]，使用 [`socket.connect(path[, connectListener])`][`socket.connect(path)`] 立即初始化连接，然后返回初始化连接的 `net.Socket`。
