<!-- YAML
added: v0.7.0
-->

* `request` {http.IncomingMessage} HTTP 请求的参数，与 [`'request'`] 事件中的一样。
* `socket` {stream.Duplex} 服务器和客户端之间的网络套接字。
* `head` {Buffer} 隧道流的第一个数据包（可能为空）。

每次客户端请求 HTTP `CONNECT` 方法时触发。 
如果未监听此事件，则请求 `CONNECT` 方法的客户端将关闭其连接。

此事件保证传入 {net.Socket} 类（{stream.Duplex} 的子类）的实例，除非用户指定了 {net.Socket} 以外的套接字类型。

触发此事件后，请求的套接字将没有 `'data'` 事件监听器，这意味着它需要绑定才能处理发送到该套接字上的服务器的数据。

