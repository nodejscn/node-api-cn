<!-- YAML
added: v8.0.0
changes:
  - version: v14.0.0
    pr-url: https://github.com/nodejs/node/pull/29197
    description: Work as a no-op on a stream that has already been destroyed.
-->

* `error` {Error} 将会在 `'error'` 事件中作为负载传入的错误。
* 返回: {this}

销毁流。 
可选地触发 `'error'` 事件，并触发 `'close'` 事件（除非将 `emitClose` 设置为 `false`）。 
在此调用之后，可读流将会释放所有内部的资源，并且将会忽略对 `push()` 的后续调用。 

一旦调用 `destroy()`，则不会再执行任何其他操作，并且除了 `_destroy()` 以外的其他错误都不会作为 `'error'` 触发。

实现者不应该重写此方法，而应该实现 [`readable._destroy()`][readable-_destroy]。

