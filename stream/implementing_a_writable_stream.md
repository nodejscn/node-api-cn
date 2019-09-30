
`stream.Writable` 类可用于实现 [`Writable`] 流。

自定义的 `Writable` 流必须调用 `new stream.Writable([options])` 构造函数并实现 `writable._write()` 和/或 `writable._writev()` 方法。

