<!-- YAML
added: v0.5.10
-->

* `handle` {Object}
* `backlog` {number} [`server.listen()`] 函数的通用参数。
* `callback` {Function} [`server.listen()`] 函数的通用参数。
* 返回: {net.Server}

启动一个服务器，监听已经绑定到端口、Unix 域套接字或 Windows 命名管道的给定 `handle` 上的连接。

`handle` 对象可以是服务器、套接字（任何具有底层 `_handle` 成员的东西），也可以是具有 `fd` 成员的对象，该成员是一个有效的文件描述符。

在 Windows 上不支持在文件描述符上进行监听。

