<!-- YAML
added: v0.1.98
-->

* `preserveCursor` {boolean} 如果为 `true`，则阻止光标落点被设为 `0`。

`rl.prompt()` 方法会在 `output` 流中新的一行写入 `readline.Interface` 实例配置后的 `prompt`，用于为用户提供一个可供输入的新的位置。

当被调用时，如果 `input` 流已被暂停，则 `rl.prompt()` 会恢复 `input` 流。

如果 `readline.Interface` 被创建时 `output` 被设为 `null` 或 `undefined`，则提示不会被写入。

