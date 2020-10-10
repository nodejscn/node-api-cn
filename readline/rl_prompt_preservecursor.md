<!-- YAML
added: v0.1.98
-->

* `preserveCursor` {boolean} 如果为 `true`，则阻止将光标落点重置为 `0`。

`rl.prompt()` 方法将 `readline.Interface` 实例配置的提示写入 `output` 中的新一行，以便为用户提供一个可供输入的新位置。

当调用时，如果 `input` 流已暂停，则 `rl.prompt()` 将恢复它。

如果 `readline.Interface` 创建时 `output` 被设置为 `null` 或 `undefined`，则不会写入提示。

