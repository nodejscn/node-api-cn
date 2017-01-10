
Writable streams are an abstraction for a *destination* to which data is
written.

Examples of [Writable][] streams include:

* [HTTP requests, on the client][]
* [HTTP responses, on the server][]
* [fs write streams][]
* [zlib streams][zlib]
* [crypto streams][crypto]
* [TCP sockets][]
* [child process stdin][]
* [`process.stdout`][], [`process.stderr`][]

*Note*: Some of these examples are actually [Duplex][] streams that implement
the [Writable][] interface.

All [Writable][] streams implement the interface defined by the
`stream.Writable` class.

While specific instances of [Writable][] streams may differ in various ways,
all Writable streams follow the same fundamental usage pattern as illustrated
in the example below:

```js
const myStream = getWritableStreamSomehow();
myStream.write('some data');
myStream.write('some more data');
myStream.end('done writing data');
```

