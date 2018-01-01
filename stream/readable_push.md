
不推荐使用`readable.push('')`。

向一个不处在object mode的流压入一个`Buffer`或`Uint8Array`0字节字符串，会产生有趣的副作用。
因为调用了[`readable.push()`][stream-push]，所以会停止读进程。
然而，因为参数是一个空字符串，没有可读的数据添加到可读buffer, 所以没有可以供用户消费的数据。
