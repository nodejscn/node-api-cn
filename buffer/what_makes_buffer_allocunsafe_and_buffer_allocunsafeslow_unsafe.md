
当调用 [`Buffer.allocUnsafe()`] 和 [`Buffer.allocUnsafeSlow()`] 时，被分配的内存段是**未初始化的**（没有用 0 填充）。
虽然这样的设计使得内存的分配非常快，但已分配的内存段可能包含潜在的敏感旧数据。
使用通过 [`Buffer.allocUnsafe()`] 创建的没有被**完全**重写内存的 `Buffer` ，在 `Buffer` 内存可读的情况下，可能泄露它的旧数据。

虽然使用 [`Buffer.allocUnsafe()`] 有明显的性能优势，但必须额外**小心**，以避免给应用程序引入安全漏洞。

