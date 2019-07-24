
[转换流]是一种[双工流]，它会对输入做些计算然后输出。
例如 [zlib] 流和 [crypto] 流会压缩、加密或解密数据。

输出流的大小、数据块的数量都不一定会和输入流的一致。
例如，`Hash` 流在输入结束时只会输出一个数据块，而 `zlib` 流的输出可能比输入大很多或小很多。
`stream.Transform` 类可用于实现了一个[转换流]。

`stream.Transform` 类继承自 `stream.Duplex`，并且实现了自有的 `writable._write()` 和 `readable._read()` 方法。
自定义的转换流必须实现 [`transform._transform()`][stream-_transform] 方法，[`transform._flush()`][stream-_flush] 方法是可选的。

当使用转换流时，如果可读端的输出没有被消费，则写入流的数据可能会导致可写端被暂停。

