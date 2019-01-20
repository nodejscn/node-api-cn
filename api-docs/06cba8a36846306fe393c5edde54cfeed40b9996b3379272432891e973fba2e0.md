<!-- YAML
added: v0.7.0
-->

* `request` {http.IncomingMessage} HTTP 请求的参数，与 [`'request'`] 事件中的一样。
* `socket` {net.Socket} 服务器和客户端之间的网络套接字。
* `head` {Buffer} 隧道流的第一个数据包（可能为空）。

每次客户端请求 HTTP `CONNECT` 方法时触发。 
如果未监听此事件，则请求 `CONNECT` 方法的客户端将关闭其连接。

触发此事件后，请求的套接字将没有 `'data'` 事件监听器，这意味着它需要绑定才能处理发送到该套接字上的服务器的数据。

