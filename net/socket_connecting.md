<!-- YAML
added: v6.1.0
-->

如果是 `true` - [`socket.connect(options[, connectListener])`][`socket.connect(options, connectListener)`] 被调用，
并且还没有完成。 在触发`connect`事件和/或调用[`socket.connect(options[, connectListener])`][`socket.connect(options, connectListener)`]
的回调函数之前，将被设置为`false` 。