<!-- YAML
added: v0.1.90
-->

* `path` {string}
* `callback` {Function}

启动一个 UNIX socket 服务器，并在给定的 `path` 上监听连接。

该函数是异步的。
`callback` 会被添加到 [`'listening'`] 事件的监听器中。也可查看 [`net.Server.listen(path)`]。

注意，`server.listen()` 方法可能被多次调用。
每次调用都会使用提供的选项重新打开服务器。

