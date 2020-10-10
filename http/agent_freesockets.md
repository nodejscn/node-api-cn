<!-- YAML
added: v0.11.4
-->

* {Object}

一个对象，其中包含当启用 `keepAlive` 时代理正在等待使用的套接字数组。 
不要修改。

`freeSockets` 列表中的 socket 会在 `'timeout' 时自动被销毁并从数组中删除。

