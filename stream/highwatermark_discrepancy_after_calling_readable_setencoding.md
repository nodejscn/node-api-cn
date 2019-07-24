
使用 `readable.setEncoding()` 会改变 `highWaterMark` 属性在非对象模式中的作用。

一般而言，当前缓冲的大小是以字节为单位跟 `highWaterMark` 比较的。
但是调用 `setEncoding()` 之后，会开始以字符为单位进行比较。

大多数情况下，使用 `latin1` 或 `ascii` 时是没有问题的。
但在处理含有多字节字符的字符串时，需要小心。

