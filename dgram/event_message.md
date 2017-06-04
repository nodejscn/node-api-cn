<!-- YAML
added: v0.1.99
-->

当有新的数据包被 socket 接收时，`'message'`事件会被触发。`msg`和`rinfo`会作为参数传递到该事件的处理函数中。
* `msg` {Buffer} - 消息
* `rinfo` {Object} - 远程地址信息
  * `address` {string} 发送方地址 
  * `family` {string} 地址类型 (`'IPv4'` or `'IPv6'`)
  * `port` {number} The sender port
  * `size` {number} The message size

