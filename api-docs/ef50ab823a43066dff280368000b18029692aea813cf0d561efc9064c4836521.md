<!-- YAML
added: v0.1.90
-->

* {Buffer}

当接收到数据的时触发该事件。`data` 参数是一个 `Buffer` 或 `String`。数据编码由 `socket.setEncoding()` 设置。（在 [Readable Stream][] 章节查看更多信息。）

注意当 `Socket` 发送 `data` 事件的时候，如果没有监听者**数据将会丢失**。
