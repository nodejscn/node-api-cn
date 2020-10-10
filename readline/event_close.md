<!-- YAML
added: v0.1.98
-->

当发生以下任一情况时会触发 `'close'` 事件：

* 调用 `rl.close()` 方法，且 `readline.Interface` 实例放弃对 `input` 流和 `output` 流的控制；
* `input` 流接收到其 `'end'` 事件；
* `input` 流接收到 `<ctrl>-D` 以发信号传输结束（EOT）；
* `input` 流接收到 `<ctrl>-C` 以发信号 `SIGINT`，并且 `readline.Interface` 实例上没有注册 `'SIGINT'` 事件监听器。

调用监听器函数不传入任何参数。

一旦触发 `'close'` 事件，则 `readline.Interface` 实例就完成了。

