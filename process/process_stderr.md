
* {Stream}

`process.stderr` 属性返回连接到`stderr`(fd `2`)的流。 
它是一个[`net.Socket`][](它是一个[Duplex][]流)，除非 fd `2`指向一个文件，在这种情况下它是一个[可写][]流。

*注意*: `process.stderr` 与其他 Node.js 流有重要的区别，详见 [note on process I/O][]。

