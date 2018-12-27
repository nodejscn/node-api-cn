<!-- YAML
added: v0.5.9
-->

* `message` {Object} JSON 对象或原始值。
* `sendHandle` {Handle} [`net.Socket`] 或 [`net.Server`] 对象，或 `undefined`。

当子进程使用 [`process.send()`] 发送消息时触发。

消息通过序列化和解析传递，收到的消息可能跟发送的不完全一样。

