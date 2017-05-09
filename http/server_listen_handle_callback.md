<!-- YAML
added: v0.5.10
-->

* `handle` {Object}
* `callback` {Function}

`handle` 对象可以被设为一个服务器或 socket（任何带有一个 `_handle` 成员的对象）、或一个 `{fd: <n>}` 对象。

该函数可以让服务器使用指定的处理程序接受连接，前提是文件描述符或处理程序已绑定了一个端口或域 socket。

Windows 平台上不支持监听文件描述符。

该函数是异步的。
`callback` 会被添加到 [`'listening'`] 事件的监听器中。也可查看 [`net.Server.listen()`]。

返回 `server`。

注意，`server.listen()` 方法可能被多次调用。
每次调用都会使用提供的选项重新打开服务器。

