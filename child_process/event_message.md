<!-- YAML
added: v0.5.9
-->

* `message` {Object} 一个已解析的 JSON 对象或原始值。
* `sendHandle` {Handle} 一个 [`net.Socket`] 或 [`net.Server`] 对象 或 `undefined`。

当一个子进程使用 [`process.send()`] 发送消息时会触发 `'message'` 事件。

*注意*: 消息通过JSON序列化和解析传递，结果就是消息可能跟开始发送的不完全一样。请查看
[the `JSON.stringify()` specification][`JSON.stringify` spec].

<a name="child_process_child_channel"></a>
