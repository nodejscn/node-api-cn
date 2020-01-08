<!-- YAML
added: v0.3.0
-->

* `error` {Error}

在接收到 `IncomingMessage` 的套接字上调用 `destroy()`。 

如果提供了 `error`，则会在套接字上触发 `'error'` 事件，并将 `error` 作为参数传给该事件上的所有监听器。

