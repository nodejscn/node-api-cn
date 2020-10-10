<!-- YAML
added: v0.1.99
-->

* 返回: {Object}

返回一个包含 socket 地址信息的对象。
对于 UDP socket，该对象将包含 `address`、`family` 和 `port` 属性。

This method throws `EBADF` if called on an unbound socket.

