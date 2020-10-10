<!-- YAML
added: v8.4.0
-->

* 继承自: {EventEmitter}

`http2.Http2Session` 类的实例代表了 HTTP/2 客户端与服务器之间的一个活跃的通信会话。 
此类的实例不是由用户代码直接地构造。

每个 `Http2Session` 实例会有略有不同的行为，这取决于它是作为服务器还是客户端运行。 
`http2session.type` 属性可用于判断 `Http2Session` 的运行模式。 
在服务器端上，用户代码应该很少有机会直接与 `Http2Session` 对象一起使用，大多数操作通常是通过与 `Http2Server` 或 `Http2Stream` 对象的交互来进行的。

用户代码不会直接地创建 `Http2Session` 实例。 
当接收到新的 HTTP/2 连接时，服务器端的 `Http2Session` 实例由 `Http2Server` 实例创建。 
客户端的 `Http2Session` 实例是使用 `http2.connect()` 方法创建的。

