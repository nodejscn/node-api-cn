<!-- YAML
added: v0.5.0
-->

Creates a new TCP or [IPC][] server.
创建一个新的TCP或[IPC][]服务。

* `options` {Object}
  * `allowHalfOpen` {boolean} 表示是否允许一个半开的TCP连接。
  **默认值:** `false`
  * `pauseOnConnect` {boolean} 一旦来了连接，是否暂停套接字。
  **默认值:** `false`
* `connectionListener` {Function} 为[`'connection'`][] 事件自动设置一个监听器。
* 返回: {net.Server}

如果 `allowHalfOpen` 被设置为`true`, 那么当[`socket.end()`][] 被显式调用时,
如果对边套接字发送了一个FIN包，服务只会返回一个FIN数据包，
这会持续到后来连接处在半闭状态 (不可读但是可写)。
请查看[`'end'`][] 事件和 [RFC 1122][half-closed] (4.2.2.13节) 获取更多信息。

如果 `pauseOnConnect` 被设置为 `true`, 那么与连接相关的套接字都会暂停，也不会从套接字句柄读取数据。
这样就允许连接在进程之间传递，避免数据被最初的进程读取。
如果想从一个暂停的套接字开始读数据，请调用[`socket.resume()`][]

服务可以是一个TCP服务或者一个 [IPC][] 服务,
这取决于[`listen()`][`server.listen()`] 监听什么

这是一个简单的TCP回声服务器在8124端口上监听连接的例子：

```js
const net = require('net');
const server = net.createServer((c) => {
  // 'connection' listener
  console.log('client connected');
  c.on('end', () => {
    console.log('client disconnected');
  });
  c.write('hello\r\n');
  c.pipe(c);
});
server.on('error', (err) => {
  throw err;
});
server.listen(8124, () => {
  console.log('server bound');
});
```

用 `telnet`测试:

```console
$ telnet localhost 8124
```

想监听 `/tmp/echo.sock` 只需改最后三行为：

```js
server.listen('/tmp/echo.sock', () => {
  console.log('server bound');
});
```

用 `nc` 连一个 UNIX 域套接字服务器:

```console
$ nc -U /tmp/echo.sock
```
