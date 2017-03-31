
可读流（Readable streams）是对提供数据的 *源头* （source）的抽象。

可读流的例子包括：

* [HTTP responses, on the client][http-incoming-message]
* [HTTP requests, on the server][http-incoming-message]
* [fs read streams][]
* [zlib streams][zlib]
* [crypto streams][crypto]
* [TCP sockets][]
* [child process stdout and stderr][]
* [`process.stdin`][]

所有的 [Readable][] 都实现了
`stream.Readable` 类定义的接口。

