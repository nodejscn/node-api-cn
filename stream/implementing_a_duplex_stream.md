
双工流(可读可写流)是[可读流](#stream_readable_streams)和[可写流](stream_writable_streams)的实现，例如TCP套接字连接。

因为JavaScript不支持多重继承，所以`stream.Duplex`类被扩展以实现[双工流](#stream_class_stream_duplex)（而不是扩展`stream.Readable`和`stream.Writable`类）。

*注意。*`stream.Duplex`类原型继承来自`stream.Readable`和寄生的`stream.Writable`，但是`instanceof`将会在这两个基础类上正确工作，由于`stream.Writable`覆盖了[ Symbol.hasInstance](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Symbol/hasInstance)方法。

自定义双工流*必须*通过`new stream.Duplex([options])`构造函数并实现`readable._read()`和`writable._write()`方法。
