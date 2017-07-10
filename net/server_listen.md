
为connections启动一个 server 监听. 一个 `net.Server` 可以是一个 TCP 或者 
一个 [IPC][] server，这取决于它监听什么。

Possible signatures:

* [`server.listen(handle[, backlog][, callback])`][`server.listen(handle)`]
* [`server.listen(options[, callback])`][`server.listen(options)`]
* [`server.listen(path[, backlog][, callback])`][`server.listen(path)`]
  for [IPC][] servers
* [`server.listen([port][, host][, backlog][, callback])`][`server.listen(port, host)`]
  for TCP servers

这个函数是异步的。当 server 开始监听，[`'listening'`][] 事件会触发。最后一个参数
`callback` 将会被添加为[`'listening'`][] 事件的监听器。


所有的 `listen()` 方法可以传入一个 `backlog` 参数来指定待连接队列的最大长度。
实际长度将通过 OS 的 sysctl 设置， 例如 linux 里的 `tcp_max_syn_backlog` 和 `somaxconn`。
这个参数的默认值是511 (不是512）

*说明*：

* 所有的[`net.Socket`][] 被设置为 `So_REUSEADDR` (详见 [socket(7)][])

* `server.listen()` 方法可能会被调用多次. 通过先前提供的选项, 每个 subsequent call 将会 *re-open* 该 server

监听时，其中一个最常引发的错误是 `EADDRINUSE`。
这发生在当另一个 server 已经监听了该请求中的 `port` / `path` / `handle`。
处理这种情况的一种方法是在一定时间后重试：

```js
server.on('error', (e) => {
  if (e.code === 'EADDRINUSE') {
    console.log('Address in use, retrying...');
    setTimeout(() => {
      server.close();
      server.listen(PORT, HOST);
    }, 1000);
  }
});
```

