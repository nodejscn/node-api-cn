<!-- YAML
added: v6.1.0
-->

如果为 `true` 则[`socket.connect(options[, connectListener])`][`socket.connect(options)`] 被调用但还未结束。当发送 `connect` 事件或调用 [`socket.connect(options[, connectListener])`][`socket.connect(options)`] 的回调函数的时候会被设置为 `false`。
