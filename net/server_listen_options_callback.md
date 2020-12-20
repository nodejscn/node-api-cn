<!-- YAML
added: v0.11.14
changes:
  - version: v11.4.0
    pr-url: https://github.com/nodejs/node/pull/23798
    description: The `ipv6Only` option is supported.
-->

* `options` {Object} 必须。支持以下参数属性：
  * `port` {number}
  * `host` {string}
  * `path` {string} 如果指定了 `port` 参数则会被忽略。查看[识别 IPC 连接的路径。][Identifying paths for IPC connections]。
  * `backlog` {number} [`server.listen()`] 函数的通用参数。
  * `exclusive` {boolean} **默认值:** `false`。
  * `readableAll` {boolean} 对于 IPC 服务器，使管道对所有用户都可读。**默认值:** `false`。
  * `writableAll` {boolean} 对于 IPC 服务器，使管道对所有用户都可写。**默认值:** `false`。
  * `ipv6Only` {boolean} 对于 TCP 服务器，将 `ipv6Only` 设置为 `true` 将会禁用双栈支持，即绑定到主机 `::` 不会使 `0.0.0.0` 绑定。**默认值:** `false`。
* `callback` {Function}
* 返回: {net.Server}

<!--lint disable no-undefined-references-->
如果指定了 `port` 参数，该方法的行为跟 [server.listen([port[, host[, backlog]]][, callback])][server_listen_port] 一样。
否则，如果指定了 `path` 参数，该方法的行为与 [`server.listen(path[, backlog][, callback])`][`server.listen(path)`] 一致。
如果没有 `port` 或者 `path` 参数，则会抛出一个错误。
<!--lint enable no-undefined-references-->

如果 `exclusive` 是 `false`（默认），则集群的所有进程将使用相同的底层句柄，允许共享连接处理任务。如果 `exclusive` 是 `true`，则句柄不会被共享，如果尝试端口共享将导致错误。监听独立端口的例子如下。

```js
server.listen({
  host: 'localhost',
  port: 80,
  exclusive: true
});
```

以 root 身份启动 IPC 服务器可能导致无特权用户无法访问服务器路径。 
使用 `readableAll` 和 `writableAll` 将使所有用户都可以访问服务器。

