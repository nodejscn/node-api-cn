
Initiate a connection on a given socket.

Possible signatures:

* [socket.connect(options[, connectListener])][`socket.connect(options)`]
* [socket.connect(path[, connectListener])][`socket.connect(path)`]
  for [IPC][] connections.
* [socket.connect(port[, host][, connectListener])][`socket.connect(port, host)`]
  for TCP connections.
* Returns: {net.Socket} The socket itself.

This function is asynchronous. When the connection is established, the
[`'connect'`][] event will be emitted. If there is a problem connecting,
instead of a [`'connect'`][] event, an [`'error'`][] event will be emitted with
the error passed to the [`'error'`][] listener.
The last parameter `connectListener`, if supplied, will be added as a listener
for the [`'connect'`][] event **once**.


在给定的套接字上启动一个连接。

可能的签名：

* [socket.connect(options[, connectListener])][`socket.connect(options)`]
* [socket.connect(path[, connectListener])][`socket.connect(path)`] 用于 [IPC][] 连接。
* [socket.connect(port[, host][, connectListener])][`socket.connect(port, host)`] 用于 TCP 。
* Returns: {net.Socket} socket 自身。

This function is asynchronous. When the connection is established, the
[`'connect'`][] event will be emitted. If there is a problem connecting,
instead of a [`'connect'`][] event, an [`'error'`][] event will be emitted with
the error passed to the [`'error'`][] listener.
The last parameter `connectListener`, if supplied, will be added as a listener
for the [`'connect'`][] event **once**.

该方法是异步的。当连接建立了的时候，[`'connect'`][] 事件将会被触发。如果连接过程中有问题，[`'error'`][] 事件将会代替 [`'connect'`][] 事件被触发，并将错误信息传递给 [`'error'`][] 监听器。
