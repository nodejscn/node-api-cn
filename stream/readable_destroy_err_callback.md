<!-- YAML
added: v8.0.0
-->

* `err` {Error} 错误。
* `callback` {Function} 回调函数，第一个参数为`err`参数。

`_destroy()`需通过[`readable.destroy()`][readable-destroy]方法调用。它可以被子类覆盖，但不能直接调用。
