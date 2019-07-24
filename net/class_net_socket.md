<!-- YAML
added: v0.3.4
-->


此类是 TCP 套接字或流式 [IPC] 端点的抽象（在 Windows 上使用命名管道，否则使用 UNIX 域套接字）。 
`net.Socket` 也是[双工流][duplex stream]，因此它既可读也可写，也是一个 [`EventEmitter`]。

`net.Socket` 可以由用户创建并直接用于与服务器交互。 
例如，它由 [`net.createConnection()`] 返回，因此用户可以使用它与服务器通信。

它也可以由 Node.js 创建，并在收到连接时传给用户。 
例如，它被传给 [`net.Server`] 上触发的 [`'connection'`] 事件的监听器，因此用户可以使用它与客户端进行交互。

