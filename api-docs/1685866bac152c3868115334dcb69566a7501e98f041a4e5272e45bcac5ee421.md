<!-- YAML
added: v0.1.0
-->

* `socket` {net.Socket}

建立新的 TCP 流时会触发此事件。 
`socket` 通常是 [`net.Socket`] 类型的对象。 
通常用户无需访问此事件。 
特别是，由于协议解析器附加到套接字的方式，套接字将不会触发 `'readable'` 事件。 
也可以通过 `request.connection` 访问 `socket`。

用户也可以显式触发此事件，以将连接注入 HTTP 服务器。 
在这种情况下，可以传入任何 [`Duplex`] 流。

