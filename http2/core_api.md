
核心 API 提供了专门针对支持 HTTP/2 协议的特性而设计的底层接口。 
它不是专门设计为与现有的 [HTTP/1] 模块 API 兼容。 
当然，也有[兼容的 API][Compatibility API]。

`http2` 核心 API 在客户端和服务器之间比 `http` API 更加对称。 
例如，大多数事件，比如 `'error'`、`'connect'` 和 `'stream'`，都可以由客户端代码或服务器端代码触发。

