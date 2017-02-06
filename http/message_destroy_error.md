<!-- YAML
added: v0.3.0
-->

* `error` {Error}

调用接收 `IncomingMessage` 的 socket 的 `destroy()`。
如果提供了 `error`，则触发 `'error'` 事件，且把 `error` 作为一个参数传入事件的任何监听器。

