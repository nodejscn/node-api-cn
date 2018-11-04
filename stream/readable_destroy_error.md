<!-- YAML
added: v8.0.0
-->

* `error` {Error} 传给 `'error'` 事件的错误对象。
* 返回: {this}

销毁流，并触发 `'error'` 事件和 `'close'` 事件。
调用后，可读流将释放所有的内部资源，且忽视后续的 `push()` 调用。
实现流时不应该重写这个方法，而是重写 [`readable._destroy()`][readable-_destroy]。

