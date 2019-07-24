
可写流是对数据要被写入的目的地的一种抽象。

可写流的例子包括：

* [客户端的 HTTP 请求][HTTP requests, on the client]
* [服务器的 HTTP 响应][HTTP responses, on the server]
* [fs 的写入流][fs write streams]
* [zlib 流][zlib]
* [crypto 流][crypto]
* [TCP socket][TCP sockets]
* [子进程 stdin][child process stdin]
* [`process.stdout`]、[`process.stderr`]

上面的一些例子事实上是实现了可写流接口的 [`Duplex`] 流。

所有可写流都实现了 [`stream.Writable`] 类定义的接口。

尽管可写流的具体实例可能略有差别，但所有的可写流都遵循同一基本的使用模式，如以下例子所示：

```js
const myStream = getWritableStreamSomehow();
myStream.write('一些数据');
myStream.write('更多数据');
myStream.end('完成写入数据');
```

