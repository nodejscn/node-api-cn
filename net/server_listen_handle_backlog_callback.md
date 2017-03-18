<!-- YAML
added: v0.5.10
-->

* `handle` {Object}
* `backlog` {Number}
* `callback` {Function}

`handle` 对象可以被设置为服务器或者是socket（任何有着下标`_handle`属性的对象）, 或者一个 `{fd: <n>}` 对象.

这可能会导致服务器在特定的handle上接受连接，
但是它被认为文件描述器或者处理器已经被绑定到一个端口或者socket域上。

Windows系统不支持监听文件描述器。

这个函数是异步的。当服务器已经被绑定时，
[`'listening'`][] 事件将被触发.
最后一个参数`callback`将被添加为 [`'listening'`][]事件的一个监听器 .

`backlog` 参数表现的同
[`server.listen([port][, hostname][, backlog][, callback])`][`server.listen(port, host, backlog, callback)`]一样.

