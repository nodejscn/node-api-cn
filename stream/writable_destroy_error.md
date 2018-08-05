<!-- YAML
added: v8.0.0
-->

* 返回: {this}

摧毁流，并触发传入的 `'error'` 与 `'close'` 事件。
该方法被调用后，可写流就结束了，且之后调用 `write()` 或 `end()` 都会导致 `ERR_STREAM_DESTROYED` 错误。
实现流时不应该重写这个方法，而是重写 [`writable._destroy()`][writable-_destroy]。

