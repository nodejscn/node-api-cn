
* {Stream}

`process.stderr` 属性会返回连接到 `stderr` (文件描述符 `2`) 的流。 
它是一个 [`net.Socket`]（也就是 [Duplex] 流），除非文件描述符 `2` 指向文件（在这种情况下它是一个 [Writable] 流）。

`process.stderr` 与其他的 Node.js 流有重大区别。
详见[进程 I/O 的注意事项][note on process I/O]。


