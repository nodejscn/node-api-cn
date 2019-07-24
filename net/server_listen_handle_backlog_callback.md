<!-- YAML
added: v0.5.10
-->

* `handle` {Object}
* `backlog` {number} [`server.listen()`][] 的通用参数
* `callback` {Function} [`server.listen()`][] 的通用参数
* Returns: {net.Server}

启动一个服务器，监听已经绑定到端口、UNIX 域套接字或 Windows 命名管道的给定句柄上的连接。

句柄对象可以是服务器、套接字（任何具有底层 `_handle` 成员的东西），也可以是具有 `fd` 成员的对象，该成员是一个有效的文件描述符。

*注意*：在Windows上不支持在文件描述符上进行监听。
