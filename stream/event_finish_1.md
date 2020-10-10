
[`'finish'`] 事件来自 `stream.Writable` 类。
当调用了 [`stream.end()`][stream-end] 并且 [`stream._transform()`][stream-_transform] 处理完全部数据块之后，触发 `'finish'` 事件。
如果出现错误，则不应触发 `'finish'`。

