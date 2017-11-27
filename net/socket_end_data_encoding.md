<!-- YAML
added: v0.1.90
-->

* Returns: {net.Socket} Socket 本身。

半关闭 socket。例如发送一个 FIN 包。服务端仍可以发送数据。

如果指定了 `data`，则相当于调用 `socket.write(data, encoding)` 之后再调用 [`socket.end()`][]。
