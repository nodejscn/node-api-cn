<!-- YAML
added: v0.11.2
-->

调用 `writable.cork()` 方法将强制所有写入数据都存放到内存中的缓冲区里。
直到调用 [`stream.uncork()`][] 或
[`stream.end()`][stream-end] 方法时，缓冲区里的数据才会被输出。

在向流中写入大量小块数据（small chunks of data）时，内部缓冲区（internal
buffer）可能失效，从而导致性能下降。`writable.cork()` 方法主要就是用来避免这种情况。 对于这种情况，
实现了 `writable._writev()` 方法的流可以对写入的数据进行缓冲，从而提高写入效率。

也可查看 [`writable.uncork()`]。

