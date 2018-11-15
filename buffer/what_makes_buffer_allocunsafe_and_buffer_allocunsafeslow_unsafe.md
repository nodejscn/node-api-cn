
当调用 [`Buffer.allocUnsafe()`] 和 [`Buffer.allocUnsafeSlow()`] 时，分配的内存是未初始化的（没有用 0 填充）。
虽然这样的设计使得内存的分配非常快，但分配的内存可能包含旧数据。
如果没有完全地重写内存，当读取 `Buffer` 时，旧数据就泄露了。


