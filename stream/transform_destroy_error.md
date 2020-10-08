<!-- YAML
added: v8.0.0
changes:
  - version: v14.0.0
    pr-url: https://github.com/nodejs/node/pull/29197
    description: Work as a no-op on a stream that has already been destroyed.
-->

* `error` {Error}
* 返回: {this}

销毁流，并可选地触发 `'error'` 事件。
调用该方法后，transform 流会释放全部内部资源。
实现者不应该重写此方法，而应该实现 [`readable._destroy()`][readable-_destroy]。
`Transform` 流的 `_destroy()` 方法的默认实现会触发 `'close'` 事件，除非 `emitClose` 被设置为 `false`。

一旦调用 `destroy()`，则不会再执行任何其他操作，并且除了 `_destroy()` 以外的其他错误都不会作为 `'error'` 触发。

