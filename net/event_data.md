<!-- YAML
added: v0.1.90
-->

* {Buffer|string}

当接收到数据的时触发该事件。`data` 参数是一个 `Buffer` 或 `String`。数据编码由 [`socket.setEncoding()`] 设置。

当 `Socket` 触发 `'data'` 事件的时候，如果没有监听器则数据将会丢失。
