<!-- YAML
added: v0.1.94
changes:
  - version: v10.0.0
    pr-url: v10.0.0
    description: Not listening to this event no longer causes the socket
                 to be destroyed if a client sends an Upgrade header.
-->

* `request` {http.IncomingMessage} HTTP 请求的参数，与 [`'request'`] 事件中的一样。
* `socket` {net.Socket} 服务器与客户端之间的网络套接字。
* `head` {Buffer} 升级后的流的第一个数据包（可能为空）。

每次客户端请求 HTTP 升级时发出。 
监听此事件是可选的，客户端无法坚持更改协议。

触发此事件后，请求的套接字将没有 `'data'` 事件监听器，这意味着它需要绑定才能处理发送到该套接字上的服务器的数据。

