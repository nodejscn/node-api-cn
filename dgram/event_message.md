<!-- YAML
added: v0.1.99
-->

当有新的数据包被 socket 接收时，`'message'` 事件会被触发。`msg` 和 `rinfo` 会作为参数传递到该事件的处理函数中。
* `msg` {Buffer} 消息。
* `rinfo` {Object} 远程地址信息。
  * `address` {string} 发送方地址。
  * `family` {string} 地址类型 (`'IPv4'` 或 `'IPv6'`)。
  * `port` {number} 发送者端口。
  * `size` {number} 消息大小。
  
If the source address of the incoming packet is an IPv6 link local
address, the interface name is added to the `address`.  For
example, a packet received on the `en0` interface might have the
address field set to `'fe80::2618:1234:ab11:3b9c%en0'`, where `'%en0'`
is the interface name as a zone id suffix.

