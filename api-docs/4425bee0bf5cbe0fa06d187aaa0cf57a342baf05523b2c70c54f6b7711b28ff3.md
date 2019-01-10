<!-- YAML
added: v0.1.90
changes:
  - version: v6.0.0
    pr-url: https://github.com/nodejs/node/pull/6021
    description: The `hints` option defaults to `0` in all cases now.
                 Previously, in the absence of the `family` option it would
                 default to `dns.ADDRCONFIG | dns.V4MAPPED`.
  - version: v5.11.0
    pr-url: https://github.com/nodejs/node/pull/6000
    description: The `hints` option is supported now.
-->

* `options` {Object}
* `connectListener` {Function} [`socket.connect()`][] 的通用参数。将会被添加为 [`'connect'`][] 事件的监听器。
* Returns: {net.Socket} Socket 自身。

在给定的 socket 上初始化一个连接。通常该方法是不需要的，应该使用 [`net.createConnection()`][] 来创建和打开 socket。一般只在实现一个自定义的 Socket 的时候使用该方法。


对于 TCP 连接可能的 `options` 有：

* `port` {number} 必须。Socket 连接的端口。
* `host` {string} Socket 连接的主机。默认是 `'localhost'`.
* `localAddress` {string} Socket 连接的本地地址。
* `localPort` {number} Socket 连接的本地端口。
* `family` {number} IP栈的版本，可以是4或6。默认值为4。
* `hints` {number} 可选的[`dns.lookup()` hints][].
* `lookup` {Function} 自定义的 lookup 方法。默认是 [`dns.lookup()`][].

对于 [IPC][] 连接可能的 `options` 有：

* `path` {string} 必须。客户端连接的路径。查看 [Identifying paths for IPC connections][]。如果提供了，则以上的 TCP 选项都会被忽略。

返回 `socket`.
