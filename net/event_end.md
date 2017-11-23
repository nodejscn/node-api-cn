<!-- YAML
added: v0.1.90
-->

当 socket 的另一端发送一个 FIN 包的时候触发，从而结束 socket 的可读端。

默认情况下（`allowHalfOpen`为`false`），socket 将发送一个 FIN 数据包，并且一旦写出它的等待写入队列就销毁它的文件描述符。当然，如果 `allowHalfOpen` 为 `true`，socket 就不会自动结束 [`end()`][`socket.end()`] 它的写入端，允许用户写入任意数量的数据。用户必须调用 [`end()`][`socket.end()`] 显示地结束这个连接（例如发送一个 FIN 数据包。）
