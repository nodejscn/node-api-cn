<!-- YAML
added: v0.11.2
-->

The `writable.cork()` method forces all written data to be buffered in memory.
The buffered data will be flushed when either the [`stream.uncork()`][] or
[`stream.end()`][stream-end] methods are called.

The primary intent of `writable.cork()` is to avoid a situation where writing
many small chunks of data to a stream do not cause a backup in the internal
buffer that would have an adverse impact on performance. In such situations,
implementations that implement the `writable._writev()` method can perform
buffered writes in a more optimized manner.

