[`'finish'`] 事件来自 `stream.Writable` 类，[`'end'`] 事件来自 `stream.Readable` 类。
当调用了 [`stream.end()`][stream-end] 并且 [`stream._transform()`][stream-_transform] 处理完全部数据块之后，触发 `'finish'` 事件。
当调用了 [`transform._flush()`][stream-_flush] 中的回调函数并且所有数据已经输出之后，触发 `'end'` 事件。

