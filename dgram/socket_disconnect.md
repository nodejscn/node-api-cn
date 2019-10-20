<!-- YAML
added: v12.0.0
-->

一个将相连的 `dgram.Socket` 与远程地址断掉的同步函数。
在一个已经未连接的 socket 上尝试调用 `disconnect()` 会导致一个 [`ERR_SOCKET_DGRAM_NOT_CONNECTED`][] 异常。
