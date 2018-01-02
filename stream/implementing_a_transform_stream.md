
一个[Transform][]流是一种[Duplex][]流，输入经过[Transform][]流，做某种计算然后输出。
比如 [zlib][]流和[crypto][]流会做压缩，加密和解密数据。

*注意*: 输出流的大小，有多少数据包，到达时间都不一定非要和输入流一样。
比如，一个哈希流再输入结束时永远只会输出单个数据块；
而一个`zlib`流的输出，可能比输入大得多或小得多。

`stream.Transform` 类被扩展了，实现了一个[Transform][]流。

The `stream.Transform` class prototypically inherits from `stream.Duplex` and
implements its own versions of the `writable._write()` and `readable._read()`
methods. Custom Transform implementations *must* implement the
[`transform._transform()`][stream-_transform] method and *may* also implement
the [`transform._flush()`][stream-_flush] method.

`stream.Transform`类最初继承自`stream.Duplex`，并且实现了它自己版本的`writable._write()`和`readable._read()`方法。
一般地，变换流*必须*实现[`transform._transform()`][stream-_transform] 方法；
而[`transform._flush()`][stream-_flush] 方法是*非必须*的。

*注意*: 用变换流时要注意，如果读端输出没有被消费，那么往写数据可能会引起写端暂停。

