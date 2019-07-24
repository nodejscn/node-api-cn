<!-- YAML
added: v0.3.0
-->

* `error` {Error}

在接收 `IncomingMessage` 的套接字上调用 `destroy()`。 
如果提供了 `error`，则会触发 `'error'` 事件，并将 `error` 作为参数传递给事件上的任何监听器。

