<!-- YAML
added: v0.11.13
changes:
  - version: v8.6.0
    pr-url: https://github.com/nodejs/node/pull/14560
    description: The `lookup` option is supported.
  - version: v8.7.0
    pr-url: https://github.com/nodejs/node/pull/13623
    description: The `recvBufferSize` and `sendBufferSize` options are
                 supported now.
-->

* `options` {Object} 允许的选项是:
  * `type` {string} 套接字族. 必须是 `'udp4'` 或 `'udp6'`.
    必需填.
  * `reuseAddr` {boolean} 若设置为 `true` [`socket.bind()`][] ，则会
    重用地址，即时另一个进程已经在其上面绑定了一个套接字。
    默认是 `false`.
  * `recvBufferSize` {number} - 设置 `SO_RCVBUF` 套接字值。
  * `sendBufferSize` {number} - 设置 `SO_SNDBUF` 套接字值。
  * `lookup` {Function} 惯常的查询函数. 默认是 [`dns.lookup()`][]。
* `callback` {Function} 为 `'message'` 事件绑定一个监听器。可选。
* 返回: {dgram.Socket}

创建一个 `dgram.Socket` 对象. 一旦创建了套接字，调用
[`socket.bind()`][] 会指示套接字开始监听数据报消息。如果 `address` 和 `port` 没传给  [`socket.bind()`][]，
那么这个方法会把这个套接字绑定到 "全部接口" 地址的一个随机端口(这适用于 `udp4` 和 `udp6` 套接字)。
绑定的地址和端口可以通过 [`socket.address().address`][] 和[`socket.address().port`][] 来获取。
