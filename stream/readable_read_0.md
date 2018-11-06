
在某些情况下，需要触发底层可读流的刷新，但实际并不消费任何数据。
在这种情况下，可以调用 `readable.read(0)`，返回 `null`。

如果内部读取缓冲小于 `highWaterMark`，且流还未被读取，则调用 `stream.read(0)` 会触发调用底层的 [`stream._read()`][stream-_read]。

虽然大多数应用程序几乎不需要这样做，但 Node.js 中会出现这种情况，尤其是在可读流类的内部。

