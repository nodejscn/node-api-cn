<!-- YAML
added: v0.1.94
-->

* `request` {http.IncomingMessage} HTTP 请求的参数，与 [`'request'`] 事件的相同
* `socket` {net.Socket} 服务器与客户端之间的网络 socket
* `head` {Buffer} 升级流的第一个数据包（可能为空）

每当一个客户端请求一个 HTTP 升级时触发。
如果该事件未被监听，则发送升级的客户端会关闭它们的连接。

当该事件被触发后，请求的 socket 不会有 `'data'` 事件监听器，也就是说需要绑定它以用来处理 socket 上被发送到服务器的数据。

