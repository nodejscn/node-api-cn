<!-- YAML
added: v0.3.4
-->

`rl.pause()` 方法会暂停 `input` 流，允许稍后在必要时恢复它。

调用 `rl.pause()` 不会立刻暂停 `readline.Interface` 实例触发的其他事件（包括 `'line'`）。

