<!-- YAML
changes:
  - version: v12.11.0
    pr-url: https://github.com/nodejs/node/pull/29639
    description: _write() is optional when providing _writev().
-->

* `chunk` {Buffer|string|any} 要写入的 `Buffer`，从传给 [`stream.write()`][stream-write] 的 `string` 转换而来。 
   如果流的 `decodeStrings` 选项为 `false` 或者流在对象模式下运行，则数据块将不会被转换，并且将是传给 [`stream.write()`][stream-write] 的任何内容。
* `encoding` {string} 如果 `chunk` 是字符串，则指定字符编码。
  如果 `chunk` 是 `Buffer` 或者流处于对象模式，则无视该选项。
* `callback` {Function} 当数据块被处理完成后的回调函数。

所有可写流的实现必须提供 [`writable._write()`][stream-_write] 和/或 [`writable._writev()`][stream-_writev] 方法将数据发送到底层资源。

[`Transform`] 流会提供自身实现的 [`writable._write()`][stream-_write]。

该函数不能被应用程序代码直接调用。
它应该由子类实现，且只能被内部的 `Writable` 类的方法调用。

必须在 `writable._write()` 内部同步地调用、或异步地（即不同的时间点）调用 `callback` 函数，以表明写入成功完成或因错误而失败。
如果调用失败，则 `callback` 的第一个参数必须是 `Error` 对象。
如果写入成功，则 `callback` 的第一个参数为 `null`。

在 `writable._write()` 被调用之后且 `callback` 被调用之前，所有对 `writable.write()` 的调用都会把要写入的数据缓冲起来。
当调用 `callback` 时，流将会触发 [`'drain'`]事件。
如果流的实现需要同时处理多个数据块，则应该实现 `writable._writev()` 方法。

如果在构造函数选项中设置 `decodeStrings` 属性为 `false`，则 `chunk` 会保持原样传入 `.write()`，它可能是字符串而不是 `Buffer`。
这是为了实现对某些特定字符串数据编码的支持。 
在这种情况下，`encoding` 参数将指示字符串的字符编码。 否则，可以安全地忽略编码参数。

`writable._write()` 方法有下划线前缀，因为它是在定义在类的内部，不应该被用户程序直接调用。

