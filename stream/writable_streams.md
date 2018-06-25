
可写流是对数据要写入的目的地的一种抽象。

[可写流]的例子包括：

* [客户端上的 HTTP 请求][HTTP requests, on the client]
* [服务器上的 HTTP 响应][HTTP responses, on the server]
* [fs 写入的流][fs write streams]
* [zlib 流][zlib]
* [crypto 流][crypto]
* [TCP socket][TCP sockets]
* [child process stdin]
* [`process.stdout`]、[`process.stderr`]

上面的某些例子事实上是实现了 [`Writable`] 接口的 [`Duplex`] 流。

所有的[可写流]都实现了 `stream.Writable` 类定义的接口。

尽管[可写流]的具体实现可能略有差别，但所有的可写流都遵循同一基本的使用模式，如下面例子所示：

```js
const myStream = getWritableStreamSomehow();
myStream.write('some data');
myStream.write('some more data');
myStream.end('done writing data');
```

