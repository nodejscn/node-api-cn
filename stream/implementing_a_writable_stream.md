这个`stream.Writeable`类被用于实现可写流。

自定义可写流必须调用`new stream.Writeable([options])`构造函数并且实现`writeable._write()`方法。`writeable._writev()`方法也是可以实现的。

