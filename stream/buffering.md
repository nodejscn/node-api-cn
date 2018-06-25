
<!--type=misc-->

[`Writable`] 和 [`Readable`] 流都会在内部的缓冲器中存储数据，可以使用相应的 `writable.writableBuffer` 或 `readable.readableBuffer` 来获取。

可缓冲的数据的大小取决于传递给流构造函数的 `highWaterMark` 选项。
对于普通的流， `highWaterMark` 选项指定了[字节的总大小][hwm-gotcha]。
对于在对象模式中操作的流，`highWaterMark` 指定了对象的总数。

当可读流的实现调用 [`stream.push(chunk)`][stream-push] 方法时，数据会被缓冲。
如果流的消费者没有调用 [`stream.read()`][stream-read] 方法，则这些数据会始终存在于内部队列中，直到被消费。

当内部的可读缓冲的总大小达到 `highWaterMark` 指定的阈值时，流会暂停从底层资源读取数据，直到当前缓冲器的数据被消费（也就是说，流会停止调用内部的用来填充可读缓冲的 `readable._read()` 方法）。

当可写流反复调用 [`writable.write(chunk)`][stream-write] 方法时，数据会被缓冲。
当内部的可写缓冲的总大小小于 `highWaterMark` 指定的阈值时，调用 `writable.write()` 会返回`true`。 
一旦内部缓冲的大小达到或超过 `highWaterMark` 时，调用 `writable.write()` 会返回 `false`。

`stream` API 的主要目标，特别是 [`stream.pipe()`] 方法，是为了限制数据的缓冲，以达到可接受的程度，也就是读写速度不匹配的源头和目标不会超出可用的内存大小。

因为 [`Duplex`] 和 [`Transform`] 都是可读可写的，所以它们各自维护着两个相互独立的内部缓冲器用于读取和写入，
这使得它们在维护着合理高效的数据流的同时，对于读取和写入两边可以独立进行而互不影响。
例如， [`net.Socket`] 实例是 [`Duplex`] 流，它的可读端可以消费从 socket 接收的数据，而可写端则可以将数据写入到 socket。
因为数据写入到 socket 的速度可能比从 socket 接收数据的速度快或者慢，所以在读写两端独立地进行操作或缓冲就显得很重要了。

