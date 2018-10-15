<!-- YAML
added: v0.11.2
-->

强制把所有写入的数据都缓冲到内存中。
当调用 [`stream.uncork()`][] 或 [`stream.end()`][stream-end] 时，缓冲的数据才会被输出。

当写入大量小块数据到流时，内部缓冲可能失效，从而导致性能下降，`writable.cork()` 主要用于避免这种情况。
对于这种情况，实现了 `writable._writev()` 的流可以用更优的方式对写入的数据进行缓冲。


