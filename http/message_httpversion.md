<!-- YAML
added: v0.1.1
-->

* {string}

在服务器请求中，该属性返回客户端发送的 HTTP 版本。
在客户端响应中，该属性返回连接到的服务器的 HTTP 版本。
可能的值有 `'1.1'` 或 `'1.0'`。

`message.httpVersionMajor` 返回 HTTP 版本的第一个整数值，`message.httpVersionMinor` 返回 HTTP 版本的第二个整数值。

