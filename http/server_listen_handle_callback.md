<!-- YAML
added: v0.5.10
-->

* `handle` {Object}
* `callback` {Function}

`handle` 对象可以被设为一个服务器或 socket (任何以下划线开头的 `_handle` 成员)、或一个 `{fd: <n>}` 对象。

这会使服务器以指定的句柄接受连接，但假定文件描述符或句柄已经被绑定到了端口或者域 socket。

Windows 平台上不支持监听文件描述符。

该函数是异步的。
`callback` 会被添加到 [`'listening'`] 事件的监听器中。详见 [`net.Server.listen()`]。

返回 `server`。

注意，`server.listen()` 方法可能被多次调用。
每次调用都会使用提供的选项**重新打开**服务器。

