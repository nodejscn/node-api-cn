<!-- YAML
added: v0.9.2
-->

`'newSession'` 事件在创建一个新的 TLS 会话时触发。
这可能用于在外部存储保存会话。
监听器回调被调用时传入三个参数：

* `sessionId` - TLS 会话识别符。
* `sessionData` - TLS 会话数据。
* `callback` {Function} 在安全连接时为了发送或者接收数据，无参的回调函数必须被调用。

添加监听器后，监听器只在连接建立后生效。

