<!-- YAML
added: v8.0.0
-->

* `err` {Error} 错误。
* `callback` {Function} 回调函数，`err`参数可选。

通过 [`writable.destroy()`][writable-destroy] 方法调用`_destroy()`。它可以被子类覆盖，但**不能**直接调用。
