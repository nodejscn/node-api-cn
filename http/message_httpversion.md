<!-- YAML
added: v0.1.1
-->

* {string}


在服务器请求的情况下，表示客户端发送的 HTTP 版本。 
在客户端响应的情况下，表示连接到的服务器的 HTTP 版本。 
可能是 `'1.1'` 或 `'1.0'`。

另外，`message.httpVersionMajor` 是第一个整数，`message.httpVersionMinor` 是第二个整数。

