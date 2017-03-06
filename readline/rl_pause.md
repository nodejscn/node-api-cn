<!-- YAML
added: v0.3.4
-->

`rl.pause()` 方法会暂停 `input` 流，且稍后需要时可被恢复。

调用 `rl.pause()` 不会立刻暂停其他事件（包括 `'line'`）被 `readline.Interface` 实例触发。

