<!-- YAML
added: v8.0.0
-->

* `error` {Error} 传给 `'error'` 事件的错误对象。
* 返回: {this}

销毁流。 
可选地触发 `'error'` 事件，并触发 `'close'` 事件除非 `emitClose` 设置为 `false`。 
在此调用之后，可读流将释放任何内部资源，并且将忽略对 `push()` 的后续调用。 
实现者不应该重写此方法，而是实现 [`readable._destroy()`][readable-_destroy]。

