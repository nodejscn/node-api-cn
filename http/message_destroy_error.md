<!-- YAML
added: v0.3.0
-->

* `error` {Error}

调用接收到 `IncomingMessage` 的 socket 上的 `destroy()` 方法。
如果提供了 `error`，则触发 `'error'` 事件，且把 `error` 作为参数传入事件的监听器。

