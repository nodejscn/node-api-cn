<!-- YAML
added: v8.0.0
-->

* `error` {Error}

销毁流，并触发 `'error'` 事件。
调用该方法后，transform 流会释放全部内部资源。
实现者不要重写该方法，而应该实现 [`readable._destroy()`][readable-_destroy]。
`Transform` 流的 `_destroy()` 方法的默认实现会触发 `'close'` 事件。

