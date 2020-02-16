<!-- YAML
added: v0.11.2
-->

`writable.cork()` 方法强制把所有写入的数据都缓冲到内存中。
当调用 [`stream.uncork()`][] 或 [`stream.end()`][stream-end] 方法时，缓冲的数据才会被输出。

`writable.cork()` 的主要目的是为了适应将几个数据快速连续地写入流的情况。 
`writable.cork()` 不会立即将它们转发到底层的目标，而是缓冲所有数据块，直到调用 `writable.uncork()`，这会将它们全部传给 `writable._writev()`（如果存在）。 
这可以防止出现行头阻塞的情况，在这种情况下，正在等待第一个数据块被处理的同时对数据进行缓冲。 
但是，使用 `writable.cork()` 而不实现 `writable._writev()` 可能会对吞吐量产生不利影响。

也可参阅：[`writable.uncork()`]、[`writable._writev()`][stream-_writev]。

