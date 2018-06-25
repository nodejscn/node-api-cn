
调用 `readable.setEncoding()` 会改变 `highWaterMark` 属性在非对象模式中的作用。

一般而言，我们直接将缓冲器存储的 _字节数_ 同 `highWaterMark` 相比较。然而在调用 `setEncoding()` 之后，程序会将缓冲器中存储的 _字符数_ 与 `highWaterMark` 相比较。

在通常情况下，如使用 `latin1` 或 `ascii` 时，这不成问题。但在处理可能含有多字节字符的字符串时，此行为需要当心。

