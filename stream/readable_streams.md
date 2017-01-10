
Readable streams are an abstraction for a *source* from which data is
consumed.

Examples of Readable streams include:

* [HTTP responses, on the client][http-incoming-message]
* [HTTP requests, on the server][http-incoming-message]
* [fs read streams][]
* [zlib streams][zlib]
* [crypto streams][crypto]
* [TCP sockets][]
* [child process stdout and stderr][]
* [`process.stdin`][]

All [Readable][] streams implement the interface defined by the
`stream.Readable` class.

