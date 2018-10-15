<!-- YAML
added: v8.0.0
-->

* `error` {Error}
* 返回: {this}

销毁流，并触发 `'error'` 事件且传入 `error` 参数。
调用该方法后，可写流就结束了，之后再调用 `write()` 或 `end()` 都会导致 `ERR_STREAM_DESTROYED` 错误。
实现流时不应该重写这个方法，而是重写 [`writable._destroy()`][writable-_destroy]。

