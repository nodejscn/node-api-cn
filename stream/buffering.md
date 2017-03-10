
<!--type=misc-->

[Writable][] 和 [Readable][] 流都会将数据存储到内部的缓存（buffer）中。这些缓存可以
通过相应的 `writable._writableState.getBuffer()` 或
`readable._readableState.buffer`来获取。

缓存的大小取决于传递给流构造函数的 `highWaterMark` 选项。
对于普通的流， `highWaterMark`
选项指定了总共的字节数。对于工作在对象模式的流，
`highWaterMark` 指定了对象的总数。

当可读流的实现调用 
[`stream.push(chunk)`][stream-push] 方法时，数据被放到缓存中。如果流的消费者
没有调用 [`stream.read()`][stream-read] 方法， 这些数据会始终存在于内部队列中，直到被消费。

当内部可读缓存的大小达到 `highWaterMark` 指定的阈值时，流会暂停从底层资源读取数据，直到当前
缓存的数据被消费 (也就是说，
流会在内部停止调用 `readable._read()` 来填充可读缓存)。

可写流通过反复调用
[`writable.write(chunk)`][stream-write] 方法将数据放到缓存。
当内部可写缓存的总大小小于
`highWaterMark` 指定的阈值时， 调用 `writable.write()` 将返回`true`。 
一旦内部缓存的大小达到或超过 `highWaterMark` ，调用 `writable.write()` 将返回 `false` 。

`stream` API 的关键目标， 尤其对于 [`stream.pipe()`] 方法，
就是限制缓存数据大小，以达到可接受的程度。这样，对于读写速度不匹配的源头和目标，就不会超出可用的内存大小。

[Duplex][] 和 [Transform][] 都是可读写的。
在内部，它们都维护了 *两个* 相互独立的缓存用于读和写。
在维持了合理高效的数据流的同时，也使得对于读和写可以独立进行而互不影响。
例如， [`net.Socket`][] 就是 [Duplex][] 的实例，它的可读端可以消费从套接字（socket）中接收的数据， 
可写端则可以将数据写入到套接字。
由于数据写入到套接字中的速度可能比从套接字接收数据的速度快或者慢，
在读写两端使用独立缓存，并进行独立操作就显得很重要了。

