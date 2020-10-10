
每个 `Http2Session` 实例在创建时都会与一个 [`net.Socket`] 或 [`tls.TLSSocket`] 关联。 
当 `Socket` 或 `Http2Session` 被销毁时，两者都将会被销毁。

由于 HTTP/2 协议强加了特定的序列化和处理要求，因此不建议用户代码从绑定到 `Http2Session` 的 `Socket` 实例读取数据或向其写入数据。 
这样做会使 HTTP/2 会话进入不确定的状态，从而导致会话和套接字变得不可用。

一旦将 `Socket` 绑定到 `Http2Session`，则用户代码应仅依赖于 `Http2Session` 的 API。

