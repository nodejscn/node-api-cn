
当调用 [`Buffer.allocUnsafe()`] 和 [`Buffer.allocUnsafeSlow()`] 时，分配的内存片段是未初始化的（没有被清零）。
虽然这样的设计使得内存的分配非常快，但分配的内存可能包含敏感的旧数据。
使用由 [`Buffer.allocUnsafe()`] 创建的 `Buffer` 没有完全重写内存，当读取 `Buffer` 的内存时，可能使旧数据泄露。

虽然使用 [`Buffer.allocUnsafe()`] 有明显的性能优势，但必须格外小心，以避免将安全漏洞引入应用程序。

