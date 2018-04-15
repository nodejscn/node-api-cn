<!-- YAML
added: v0.1.0
-->

* `socket` {net.Socket}

当新的 TCP 流被建立时触发。
`socket` 是一个 [`net.Socket`] 类型的对象。
通常用户无需访问该事件。
注意，因为协议解析器绑定到 socket 的方式，socket 不会触发 `'readable'` 事件。
`socket` 也可以通过 `request.connection` 访问。

*Note*: This event can also be explicitly emitted by users to inject connections
into the HTTP server. In that case, any [`Duplex`][] stream can be passed.
