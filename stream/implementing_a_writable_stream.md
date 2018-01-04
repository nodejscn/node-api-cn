这个`stream.Writable`类被用于实现可写流。

自定义可写流必须调用`new stream.Writable([options])`构造函数并且实现`writable._write()`方法。`writable._writev()`方法也是可以实现的。

