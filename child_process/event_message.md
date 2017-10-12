<!-- YAML
added: v0.5.9
-->

* `message` {Object} 一个已解析的 JSON 对象或原始值。
* `sendHandle` {Handle} 一个 [`net.Socket`] 或 [`net.Server`] 对象 或 `undefined`。

当一个子进程使用 [`process.send()`] 发送消息时会触发 `'message'` 事件。

*Note*: The message goes through JSON serialization and parsing. The resulting
message might not be the same as what is originally sent. See notes in
[the `JSON.stringify()` specification][`JSON.stringify` spec].

<a name="child_process_child_channel"></a>
