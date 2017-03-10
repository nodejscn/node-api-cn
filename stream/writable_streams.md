
Writable streams 是 *destination* 的一种抽象，这种 *destination* 允许数据写入。

[Writable][] 的例子包括了：

* [HTTP requests, on the client][]
* [HTTP responses, on the server][]
* [fs write streams][]
* [zlib streams][zlib]
* [crypto streams][crypto]
* [TCP sockets][]
* [child process stdin][]
* [`process.stdout`][], [`process.stderr`][]

*注意*: 上面的某些例子事实上是 [Duplex][] 流，只是实现了 [Writable][] 接口。

所有 [Writable][] 流都实现了
`stream.Writable` 类定义的接口。

尽管特定的 [Writable][] 流的实现可能略有差别，
所有的 Writable streams 都可以按一种基本模式进行使用，如下面例子所示：

```js
const myStream = getWritableStreamSomehow();
myStream.write('some data');
myStream.write('some more data');
myStream.end('done writing data');
```

