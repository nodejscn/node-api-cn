
* `chunk` {Buffer|string|any} 要写的块。会**一直**作为缓冲区，除非`decodeStrings`选项设置为`false`或者流以对象模式运行。
* `encoding` {string} 如果块是字符串，那么`encoding`就是该字符串的字符编码。 如果块是`Buffer`，或者是流在对象模式下运行，`encoding`可能被忽略。
* `callback` {Function} 调用此函数（`err`参数可选）当块处理完成时。

所有可写流实现必须提供一个 [`writable._write()`][stream-_write] 方法将数据发送到底层资源。

*注意*：[Transform][] 流提供自己实现的[`writable._write()`][stream-_write]。

*注意*：此函数不得直接由应用程序代码调用。 它应该由子类实现，并由内部的Writable类方法调用。

必须调用`callback`方法来表示写完成成功或失败，出现错误。`callback`第一个参数必须是`Error`对象如果调用失败，成功时为`null`。

需要重点注意的是，所有`writable._write()`被调用并且`callback`被调用将导致要缓冲的写入数据。 一旦调用`callback`，流将会执行[`'drain'`] []事件。 如果想让流实现一次能够处理多个数据块，`writable._writev()`方法应该被实现。

如果在构造函数选项中设置`decodeStrings`属性，那么`chunk`可能是一个字符串而不是一个缓冲区，`encodeing`将会表示字符串的字符编码。 这是为了支持对某些字符串具有优化处理的实现数据编码。 如果`decodeStrings`属性显式设置为`false`，`encoding`参数可以安全地忽略，`chunk`将保持不变传递给`.write()`的对象。

`writable._write()`方法前缀为下划线，因为它是在定义它的类的内部，不应该直接调用用户程序。
