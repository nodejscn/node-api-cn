<!-- YAML
added: v8.0.0
-->

销毁这个流，发射`'error'`事件。
调用这个之后，变换流会释放全部内部资源
实现者不应该重载此方法，而应该实现[`readable._destroy`][readable-_destroy]。
`Transform`的默认`_destroy`实现也发射`'close'`事件。

