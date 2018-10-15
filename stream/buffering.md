
<!--type=misc-->

[可写流]和[可读流]都会在内部的缓冲器中存储数据，可以分别使用的 `writable.writableBuffer` 或 `readable.readableBuffer` 来获取。

可缓冲的数据大小取决于传入流构造函数的 `highWaterMark` 选项。
对于普通的流，`highWaterMark` 指定了[字节的总数][hwm-gotcha]。
对于对象模式的流，`highWaterMark` 指定了对象的总数。

当调用 [`stream.push(chunk)`][stream-push] 时，数据会被缓冲在可读流中。
如果流的消费者没有调用 [`stream.read()`][stream-read]，则数据会保留在内部队列中直到被消费。

一旦内部的可读缓冲的总大小达到 `highWaterMark` 指定的阈值时，流会暂时停止从底层资源读取数据，直到当前缓冲的数据被消费
（也就是说，流会停止调用内部的用于填充可读缓冲的 `readable._read()`）。

当调用 [`writable.write(chunk)`][stream-write] 时，数据会被缓冲在可写流中。
当内部的可写缓冲的总大小小于 `highWaterMark` 设置的阈值时，调用 `writable.write()` 会返回 `true`。 
一旦内部缓冲的大小达到或超过 `highWaterMark` 时，则会返回 `false`。

`stream` API 的主要目标，特别是 [`stream.pipe()`]，是为了限制数据的缓冲到可接受的程度，也就是读写速度不一致的源头与目的地不会压垮内存。

因为 [`Duplex`] 和 [`Transform`] 都是可读又可写的，所以它们各自维护着两个相互独立的内部缓冲器用于读取和写入，
这使得它们在维护数据流时，读取和写入两边可以各自独立地运作。
例如，[`net.Socket`] 实例是 [`Duplex`] 流，它的可读端可以消费从 socket 接收的数据，而可写端则可以将数据写入到 socket。
因为数据写入到 socket 的速度可能比接收数据的速度快或者慢，所以在读写两端独立地进行操作（或缓冲）就显得很重要了。


