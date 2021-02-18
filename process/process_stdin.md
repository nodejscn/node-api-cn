
* {Stream}

`process.stdin` 属性会返回连接到 `stdin` (文件描述符 `0`) 的流。 
它是一个 [`net.Socket`]（也就是 [Duplex] 流），除非文件描述符 `0` 指向文件（在这种情况下它是一个 [Readable] 流）。

关于如何从 `stdin` 中读取，详见 [`readable.read()`]。

作为 [Duplex] 流，`process.stdin` 也可以在“旧”模式中使用，该模式与在 v0.10 之前为 Node.js 编写的脚本兼容。 
详见[流的兼容性][Stream compatibility]。

在“旧”的流模式中，默认情况下 `stdin` 流是暂停的，因此必须调用 `process.stdin.resume()` 从中读取。 
注意，调用 `process.stdin.resume()` 本身会将流切换为“旧”模式。

