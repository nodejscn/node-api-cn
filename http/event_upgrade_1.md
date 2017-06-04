<!-- YAML
added: v0.1.94
-->

* `request` {http.IncomingMessage} HTTP 请求，同 [`'request'`] 事件。
* `socket` {net.Socket} 服务器与客户端之间的网络 socket。
* `head` {Buffer} 流的第一个数据包，可能为空。

每当客户端发送 HTTP `upgrade` 请求时触发。
如果该事件未被监听，则发送 `upgrade` 请求的客户端会关闭连接。

当该事件被触发后，请求的 socket 上没有 `'data'` 事件监听器，这意味着需要绑定 `'data'` 事件监听器，用来处理 socket 上被发送到服务器的数据。

