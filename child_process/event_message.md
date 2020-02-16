<!-- YAML
added: v0.5.9
-->

* `message` {Object} 一个已解析的 JSON 对象或原始值。
* `sendHandle` {Handle} 一个 [`net.Socket`] 或 [`net.Server`] 对象，或 `undefined`。

当子进程使用 [`process.send()`] 发送消息时会触发 `'message'` 事件。

消息通过序列化和解析进行传递。
收到的消息可能跟最初发送的不完全一样。

如果在衍生子进程时使用了 `serialization` 选项设置为 `'advanced'`，则 `message` 参数可以包含 JSON 无法表示的数据。 
有关更多详细信息，请参阅[高级序列化][Advanced Serialization]。


