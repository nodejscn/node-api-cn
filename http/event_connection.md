<!-- YAML
added: v0.1.0
-->

* `socket` {net.Socket}

当新的 TCP 流被建立时触发。
`socket` 是一个 [`net.Socket`] 类型的对象。
通常用户无需访问该事件。
因为协议解析器绑定到 socket 的方式，socket 不会触发 `'readable'` 事件。
`socket` 也可以通过 `request.connection` 访问。

该事件也可以通过注入连接到 HTTP 服务器显式地调用。
在这种情况下，可以传入 [`Duplex`] 流。

