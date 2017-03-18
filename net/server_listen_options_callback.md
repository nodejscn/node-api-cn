<!-- YAML
added: v0.11.14
-->

* `options` {Object} - 必须. 支持以下参数：
  * `port` {Number} - 可选.
  * `host` {String} - 可选.
  * `backlog` {Number} - 可选.
  * `path` {String} - 可选.
  * `exclusive` {Boolean} - 可选.
* `callback` {Function} - 可选.

`port`, `host`, 和 `backlog` 是 `options` 的参数,
可选的 callback 函数, 表现的好像它们在调用
[`server.listen([port][, hostname][, backlog][, callback])`][`server.listen(port, host, backlog, callback)`].
另外,  `path` 参数可以用于确定UNIX套接字。

如果 `exclusive` 是 `false` (默认), 那么cluster的worker对象将利用相同的基础处理方法，
允许共享连接处理机制。当`exclusive` 是 `true`, 处理方法不被共享，企图共享端口将导致错误。
下面是一个监听专用端口的例子：

```js
server.listen({
  host: 'localhost',
  port: 80,
  exclusive: true
});
```

*注意*: `server.listen()` 方法可能被多次调用. 每个随后的
调用将利用提供的参数 *重新打开* 服务器。

