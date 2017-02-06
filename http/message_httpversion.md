<!-- YAML
added: v0.1.1
-->

* {String}

当服务器请求时，HTTP 版本由客户端发送。
当客户端响应时，HTTP 版本由所连接的服务器发送。
可能的值有 `'1.1'` 或 `'1.0'`。

`message.httpVersionMajor` 是第一个整数，`message.httpVersionMinor` 是第二个整数。

