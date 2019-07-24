
`stream.Writable` 类可用于实现可写流。

自定义的可写流必须调用 `new stream.Writable([options])` 构造函数并实现 `writable._write()` 方法，`writable._writev()` 方法是可选的。

