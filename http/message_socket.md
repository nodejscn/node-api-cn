<!-- YAML
added: v0.3.0
-->

* {stream.Duplex}


与连接关联的 [`net.Socket`] 对象。

通过 HTTPS 的支持，使用 [`request.socket.getPeerCertificate()`] 获取客户端的身份验证详细信息。

此属性保证是 {net.Socket} 类（{stream.Duplex} 的子类）的实例，除非用户指定了 {net.Socket} 以外的套接字类型。

