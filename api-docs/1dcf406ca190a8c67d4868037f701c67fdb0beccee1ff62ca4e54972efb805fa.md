<!-- YAML
added: v0.1.90
-->

* `port` {number} 套接字应该连接的端口号. 会
  传给[`socket.connect(port[, host][, connectListener])`][`socket.connect(port, host)`].
  
* `host` {string} 套接字应该连接的主机名. 会
  传给[`socket.connect(port[, host][, connectListener])`][`socket.connect(port, host)`].
   **默认:** `'localhost'`
* `connectListener` {Function} 
  [`net.createConnection()`][] 的常见参数, 在初始化套接字时
  对`'connect'` 事件的"一次性"监听器， 会
  传给[`socket.connect(path[, connectListener])`][`socket.connect(port, host)`].
* 返回值: {net.Socket} 用于开启连接的新创建的套接字.

初始化一个TCP连接

这个函数用默认配置创建一个新的[`net.Socket`][]，然后[`socket.connect(port[, host][, connectListener])`][`socket.connect(port, host)`]初始化一个连接，并返回开启连接的那个 `net.Socket`。
