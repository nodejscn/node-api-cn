<!-- YAML
added: v0.1.99
-->

每当 `dgram.Socket` 可被寻址且可以接收数据时，就会触发 `'listening'` 事件。 
这会发生在，显式地使用 `socket.bind()`、或者隐式地使用 `socket.send()` 第一次发送数据。 
在 `dgram.Socket` 开始监听之前，底层的系统资源并不存在，且诸如 `socket.address()` 和 `socket.setTTL()` 之类的调用都会失败。

