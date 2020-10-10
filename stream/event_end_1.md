
[`'end'`] 事件来自 `stream.Readable` 类。
当调用了 [`transform._flush()`][stream-_flush] 中的回调函数并且所有数据已经输出之后，触发 `'end'` 事件。
如果出现错误，则不应触发 `'end'`。
