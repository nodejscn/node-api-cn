<!-- YAML
added: v0.1.0
-->

* `socket` {net.Socket}

当一个新的 TCP 流被建立时触发。
`socket` 是 [`net.Socket`] 类型的一个对象。
通常用户无需访问此事件。
注意，因为协议解析器绑定到 socket 上，socket 不会触发 `'readable'` 事件。
`socket` 也可以通过 `request.connection` 访问。

