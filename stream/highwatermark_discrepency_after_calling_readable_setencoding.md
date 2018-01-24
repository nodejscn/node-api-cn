
使用`readable.setEncoding()` 将会改变`highWaterMark`在非对象模式时的运作方式。

在典型情况下, 当前缓冲器(buffer)大小是依靠`highWaterMark`以字节为单位衡量的。 但是, 在调用 `setEncoding()`后, 作为对比，缓冲器(buffer)大小将以设置的字符编码为单位衡量。

在例如以`latin1` 或 `ascii`这样的字符编码的普通情况下，这并不是一个问题。但当设置会将数据解析为字符串的多字节字符编码时，需要审慎的考虑流的行为。
