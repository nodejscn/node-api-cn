<!-- YAML
added: v0.11.14
-->

* `options` {Object} 必须。支持以下参数属性：
  * `port` {number}
  * `host` {string}
  * `path` {string} 如果指定了 `port` 参数则会被忽略。查看 [Identifying paths for IPC connections][]。
  * `backlog` {number} [`server.listen()`][] 的通用参数。
  * `exclusive` {boolean} 默认 `false`。
* `callback` {Function} [`server.listen()`][] 的通用参数。
* Returns: {net.Server}

如果指定了 `port` 参数，该方法的行为跟 [`server.listen([port][, hostname][, backlog][, callback])`][`server.listen(port, host)`] 一样。否则，如果指定了 `path` 参数，该方法的行为与 [`server.listen(path[, backlog][, callback])`][`server.listen(path)`] 一致。如果没有 `port` 或者 `path` 参数，则会跑出一个错误。

如果 `exclusive` 是 `false`（默认），则集群的所有进程将使用相同的底层句柄，允许共享连接处理任务。如果 `exclusive` 是 `true`，则句柄不会被共享，如果尝试端口共享将导致错误。监听独立端口的例子如下。

```js
server.listen({
  host: 'localhost',
  port: 80,
  exclusive: true
});
```

