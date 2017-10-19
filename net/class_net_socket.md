<!-- YAML
added: v0.3.4
-->

这个类是 TCP 或 UNIX Socket 的抽象（在Windows上使用命名管道，而UNIX使用域套接字）。一个`net.Socket`也是一个[duplex stream][]，所以它能被读或写，并且它也是一个[`EventEmitter`][]。

`net.Socket`可以被用户创建并直接与server通信。举个例子，它是通过[`net.createConnection()`][]返回的，所以用户可以使用它来与server通信。

当一个连接被接收时，它也能被Node.js创建并传递给用户。比如，它是通过监听在一个[`net.Server`][]上的[`'connection'`][]事件触发而获得的，那么用户可以使用它来与客户端通信。
