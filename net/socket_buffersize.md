<!-- YAML
added: v0.3.8
deprecated:
  - v14.6.0
-->

> Stability: 0 - Deprecated: Use [`writable.writableLength`][] instead.

* {integer}

此属性显示为写入而缓冲的字符数。 
缓冲器中可能包含字符串，其编码后的长度是未知的。 
因此，此数字仅是缓冲器中字节数的近似值。

`net.Socket` 具有该属性时，则 `socket.write()` 始终可用。 
这是为了帮助用户快速启动并运行。 
计算机不能总是跟上写入套接字的数据量。 
网络连接也可能太慢。 
Node.js 将会在内部将写入套接字的数据进行排队，并在可能的情况下将其发送出去。

这种内部缓冲的结果是内存可能会增加。 
对于遇到 `bufferSize` 太大或不断增加的用户，应尝试使用 [`socket.pause()`] 和 [`socket.resume()`] 来对其程序中的数据流进行节流。

