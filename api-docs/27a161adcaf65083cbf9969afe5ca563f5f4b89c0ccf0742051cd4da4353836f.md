一个用于创建 [`net.Socket`][] 的工厂函数，立即使用 [`socket.connect()`][] 初始化链接，然后返回启动连接的 `net.Socket`。

当连接建立之后，在返回的 socket 上将触发一个 [`'connect'`][] 事件。若制定了最后一个参数 `connectListener`，则它将会被添加到 [`'connect'`][] 事件作为一个监听器。

可能的签名有：

* [`net.createConnection(options[, connectListener])`][`net.createConnection(options)`]
* [`net.createConnection(path[, connectListener])`][`net.createConnection(path)`] 用于 [IPC][] 连接。
* [`net.createConnection(port[, host][, connectListener])`][`net.createConnection(port, host)`] 用于 TCP 连接。

*注意*: The [`net.connect()`][] 函数也是该函数的别名。

