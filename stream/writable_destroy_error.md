<!-- YAML
added: v8.0.0
-->

* `error` {Error} 可选，使用 `'error'` 事件触发的错误。
* 返回: {this}

销毁流。
可选地触发 `'error'`，并且触发 `'close'` 事件触发 `emitClose` 设置为 `false`。
调用该方法后，可写流就结束了，之后再调用 `write()` 或 `end()` 都会导致 `ERR_STREAM_DESTROYED` 错误。
这是销毁流的最直接的方式。 
前面对 `write()` 的调用可能没有耗尽，并且可能触发 `ERR_STREAM_DESTROYED` 错误。 
如果数据在关闭之前应该刷新，则使用 `end()` 而不是销毁，或者在销毁流之前等待 `'drain'` 事件。
实现流时不应该重写这个方法，而是重写 [`writable._destroy()`][writable-_destroy]。

