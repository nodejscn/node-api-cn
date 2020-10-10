<!-- YAML
added: v0.1.98
-->

`rl.close()` 方法会关闭 `readline.Interface` 实例，并放弃对 `input` 和 `output` 流的控制。
当调用时，将触发 `'close'` 事件。

调用 `rl.close()` 不会立即停止 `readline.Interface` 实例触发的其他事件（包括 `'line'`）。

