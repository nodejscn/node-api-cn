<!-- YAML
added: v6.1.0
-->

如果为 `true` 则 [`socket.connect(options[, connectListener])`][`socket.connect(options)`] 被调用但还未结束。
它将保持为真，直到 socket 连接，然后设置为 `false` 并触发 `'connect'` 事件。 
注意，[`socket.connect(options[, connectListener])`][`socket.connect(options)`] 的回调是 `'connect'` 事件的监听器。

