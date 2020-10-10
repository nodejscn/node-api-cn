
* `chunks` {Object[]} 要写入的多个数据块。
  每个数据块的格式为：`{ chunk: ..., encoding: ... }`。
* `callback` {Function} 当全部数据块被处理完成后的回调函数。

该函数不能被应用程序代码直接调用。
该函数应该由子类实现，且只能被内部的 `Writable` 类的方法调用。

除了在流实现中的 `writable._write()` 之外，还可以实现 `writable._writev()` 方法，其能够一次处理多个数据块。
如果已实现且之前写入的数据有缓冲，则会调用 `_writev()` 而不是 `_write()`。

`writable._writev()` 方法有下划线前缀，因为它是在定义在类的内部，不应该被用户程序直接调用。

