<!-- YAML
added: v8.7.0
-->

* `size` {integer}

设置 `SO_SNDBUF` socket 选项。
设置 socket 发送 buffer 的最大值，以字节为单位。

This method throws [`ERR_SOCKET_BUFFER_SIZE`][] if called on an unbound socket.
