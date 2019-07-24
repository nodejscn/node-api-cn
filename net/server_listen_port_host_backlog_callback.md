<!-- YAML
added: v0.1.90
-->
* `port` {number}
* `host` {string}
* `backlog` {number} [`server.listen()`][] 函数的通用参数
* `callback` {Function} [`server.listen()`][] 函数的通用参数
* Returns: {net.Server}

启动一个TCP服务监听输入的`port`和`host`。

如果`port`省略或是0，系统会随意分配一个在[`'listening'`][]事件触发后能被`server.address().port`检索的无用端口。

如果`host`省略，如果IPv6可用，服务器将会接收基于[unspecified IPv6 address][] (`::`)的连接，否则接收基于[unspecified IPv4 address][] (`0.0.0.0`)的连接

*注意*: 在大多数的系统, 监听[unspecified IPv6 address][] (`::`)可能导致`net.Server`也监听[unspecified IPv4 address][] (`0.0.0.0`).
