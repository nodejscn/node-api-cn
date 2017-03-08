<!-- YAML
added: v0.9.4
-->

* `chunk` {String|Buffer} 要写入的数据
* `encoding` {String} 如果 `chunk` 是字符串，这里指定字符编码
* `callback` {Function} 缓冲数据输出时的回调函数
* 返回： {Boolean} 如果流需要等待 `'drain'` 事件触发才能继续写入数据，这里将返回 `false` ； 否则返回 `true`。

`writable.write()` 方法向流中写入数据，并在数据处理完成后调用 `callback` 。如果有错误发生， `callback` *不一定* 会接收到这个错误作为第一个参数。要确保可靠地检测到写入错误，应该监听
`'error'` 事件。

在确认了 `chunk` 后，如果内部缓冲区的大小没有超出创建流时设定的
`highWaterMark` 阈值，函数将返回 `true` 。
如果返回值为 `false` ，应该停止向流中写入数据，直到 [`'drain'`][] 事件被触发。然而，`false` 这个返回值只是建议性的，写入流仍将无条件地接收并缓存 `chunk` 数据，即是 [`'drain'`][] 事件还没有触发。

对象模式的写入流将忽略 `encoding` 参数。

