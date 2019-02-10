
* {Stream}

`process.stderr` 属性返回连接到 `stderr` (fd `2`) 的流。 
它是一个 [`net.Socket`] 流（也就是[双工流][Duplex]），除非 fd `2` 指向一个文件，在这种情况下它是一个[可写流][Writable]。

`process.stderr` 与其他的 Node.js 流有重大区别。
有关更多信息，参阅有关[进程 I/O 的注意事项][note on process I/O]。


