<!-- YAML
added: v0.1.99
-->

* `type` {string} - 'udp4' 或 'udp6'.
* `callback` {Function} - 为 `'message'` 事件添加一个监听器。
* 返回: {dgram.Socket}

创建一个特定 `type` 的`dgram.Socket` 对象。`type`参数是`udp4` 或 `udp6`。
可选传一个回调函数，作为 `'message'` 事件的监听器。

一旦套接字被创建。调用[`socket.bind()`][] 会指示套接字开始监听数据报消息。如果 `address` 和 `port` 没传给  [`socket.bind()`][]，
那么这个方法会把这个套接字绑定到 "全部接口" 地址的一个随机端口(这适用于 `udp4` 和 `udp6` 套接字)。
绑定的地址和端口可以通过 [`socket.address().address`][] 和[`socket.address().port`][] 来获取。
