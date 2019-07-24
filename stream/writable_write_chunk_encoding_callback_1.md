
* `chunk` {Buffer|string|any} 要写入的数据块。
  会一直是 `buffer`，除非 `decodeStrings` 选项设为 `false` 或者流处于对象模式。
* `encoding` {string} 如果 `chunk` 是字符串，则指定字符编码。
  如果 `chunk` 是 `Buffer` 或者流处于对象模式，则无视该选项。
* `callback` {Function} 当数据块被处理完成后的回调函数。

所有可写流的实现必须提供 [`writable._write()`][stream-_write] 方法将数据发送到底层资源。

[`Transform`] 流会提供自身实现的 [`writable._write()`][stream-_write]。

该函数不能被应用程序代码直接调用。
它应该由子类实现，且只能被内部的 `Writable` 类的方法调用。

无论是成功完成写入还是写入失败出现错误，都必须调用 `callback`。
如果调用失败，则 `callback` 的第一个参数必须是 `Error` 对象。
如果写入成功，则 `callback` 的第一个参数为 `null`。

在 `writable._write()` 被调用之后且 `callback` 被调用之前，所有对 `writable.write()` 的调用都会把要写入的数据缓冲起来。
当调用 `callback` 时，流将会触发 [`'drain'`]事件。
如果流的实现需要同时处理多个数据块，则应该实现 `writable._writev()` 方法。

如果在构造函数选项中设置 `decodeStrings` 属性为 `false`，则 `chunk` 会保持原样传入 `.write()`，它可能是字符串而不是 `Buffer`。
这是为了实现对某些特定字符串数据编码的支持。 
当 `decodeStrings` 为 `false` 时，则 `encoding` 参数指定字符串的字符编码。 
否则，则 `encoding` 不起作用。
`writable._write()` 方法有下划线前缀，因为它是在定义在类的内部，不应该被用户程序直接调用。

