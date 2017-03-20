<!-- YAML
added: v0.1.90
-->

半关闭socket. 即它将发送一个FIN包. 服务器仍然可能发送一些数据。

如果`data`是指定的，它等价于调用`socket.write(data, encoding)`，
之后在调用`socket.end()`.
