[`'finish'`][]事件来自`stream.Writable`；[`'end'`][]事件来自`stream.Readable`类。

在调用了[`stream.end()`][stream-end]并且[`stream._transform()`][stream-_transform]处理了全部数据块之后，
`'finish'`事件触发。

[`transform._flush()`][stream-_flush]中的回调函数被调用之后，所有数据已经输出，此时，`'end'`事件触发

