
`stream.Readable` 类可用于实现可读流。 

自定义的可读流必须调用 `new stream.Readable([options])` 构造函数并实现 `readable._read()` 方法。

