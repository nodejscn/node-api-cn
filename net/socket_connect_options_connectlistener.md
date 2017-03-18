<!-- YAML
added: v0.1.90
-->

根据给定的socket参数，打开连接.

对于TCP socket, `options`参数应该是一个对象，它确定了:

  - `port`: 客户端应该连接的端口(必须).

  - `host`: 客户端应该连接的host主机. 默认为`'localhost'`.

  - `localAddress`: 为了网络连接应该绑定的本地接口。

  - `localPort`: 为了网络连接应该绑定的本地端口.

  - `family` : IP地址族的.默认为 `4`.

  - `hints`: [`dns.lookup()` hints][]. 默认为 `0`.

  - `lookup` : 可定制查询函数. 默认为 `dns.lookup`.

对于本地域socket, `options` 参数 应当是一个参数，它确定了:

  - `path`: 客户端应该连接的路径 (必须).

正常地，这个方法不是必要的，因为`net.createConnection`打开了socket。 
如果你要实现自己定制的socket才用这个方法。

这个函数是异步的。当[`'connect'`][]事件被触发时，socket已经建立。
如果有一个问题连接，`'connect'`事件将不会被触发，有异常的[`'error'`][]事件
将被触发。

`connectListener`参数将被添加为[`'connect'`][]事件的监听器。

