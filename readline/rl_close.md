<!-- YAML
added: v0.1.98
-->

`rl.close()` 方法会关闭 `readline.Interface` 实例，且撤回对 `input` 和 `output` 流的控制。
但被调用时，`'close'` 事件会被触发。

