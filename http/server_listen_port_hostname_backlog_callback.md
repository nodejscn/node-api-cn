<!-- YAML
added: v0.1.90
-->

* `port` {number}
* `hostname` {string}
* `backlog` {number}
* `callback` {Function}

开始在指定的 `port` 和 `hostname` 上接受连接。
如果省略了 `hostname`，则当 IPv6 可用时，服务器会接受 [未指定的 IPv6 地址]（`::`）的连接，否则接受 [未指定的 IPv4 地址]（`0.0.0.0`）的连接。

*请注意*: 在大多数操作系统中，监听未指定的IPv6地址[unspecified IPv6 address][] (`::`)可能会导致`net.Server`也监听未指定的IPv4地址[unspecified IPv4 address][] (`0.0.0.0`)。

如果省略了 `port` 或值为 `0`，则操作系统会分配一个随机的端口，该端口可在 `'listening'` 事件被触发后使用 `server.address().port` 获取。

若要监听一个 UNIX socket，则需提供文件名而不是端口和主机名。

`backlog` 是等待连接的队列的最大长度。
实际长度由操作系统通过 `sysctl` 设置决定，比如 Linux 上的 `tcp_max_syn_backlog` 和 `somaxconn`。
该参数的默认值是 `511`（不是 `512`）。

该函数是异步的。
`callback` 会被添加到 [`'listening'`] 事件的监听器中。也可查看 [`net.Server.listen(port)`]。

注意，`server.listen()` 方法可能被多次调用。
每次调用都会使用提供的选项重新打开服务器。

