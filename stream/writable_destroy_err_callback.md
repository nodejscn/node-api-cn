<!-- YAML
added: v8.0.0
-->

* `err` {Error} 可能发生的错误。
* `callback` {Function} 回调函数。

`_destroy()` 方法会被 [`writable.destroy()`][writable-destroy] 调用。
它可以被子类重写，但不能直接调用。

