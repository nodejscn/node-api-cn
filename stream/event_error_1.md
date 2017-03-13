<!-- YAML
added: v0.9.4
-->

* {Error}

`'error'` 事件可以在任何时候在可读流实现（Readable implementation）上触发。
通常，这会在底层系统内部出错从而不能产生数据，或当流的实现试图传递错误数据时发生。

回调函数将接收到一个 `Error` 对象。
