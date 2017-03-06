<!-- YAML
added: v0.1.98
-->

当以下之一发生时，触发 `'close'` 事件：

* `rl.close()` 方法被调用，且 `readline.Interface` 实例已撤回对 `input` 流和 `output` 流的控制；
* `input` 流接收到 `'end'` 事件；
* `input` 流接收到表示结束传输的 `<ctrl>-D`；
* `input` 流接收到表示 `SIGINT` 的 `<ctrl>-C`，且 `readline.Interface` 实例上没有注册 `SIGINT` 事件监听器。

监听器函数被调用时不传入任何参数。

当 `'close'` 事件被触发时，`readline.Interface` 实例应当被视为已结束。

