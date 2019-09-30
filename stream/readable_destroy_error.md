<!-- YAML
added: v8.0.0
-->

* `error` {Error} 将会在 `'error'` 事件中作为负载传入的错误。
* 返回: {this}

销毁流。 
可选地触发 `'error'` 事件，并触发 `'close'` 事件（除非将 `emitClose` 设置为 `false`）。 
在此调用之后，可读流将会释放所有内部的资源，并且将会忽略对 `push()` 的后续调用。 
实现者不应该重写此方法，而应该实现 [`readable._destroy()`][readable-_destroy]。

