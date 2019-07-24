<!-- YAML
added: v0.5.0
-->

* `options` {Object}
  * `allowHalfOpen` {boolean} 表明是否允许半开的 TCP 连接。**默认值:** `false`。
  * `pauseOnConnect` {boolean} 表明是否应在传入连接上暂停套接字。**默认值:** `false`。
* `connectionListener` {Function} 自动设置为 [`'connection'`] 事件的监听器。
* 返回: {net.Server}

创建一个新的 TCP 或 [IPC] 服务器。

如果 `allowHalfOpen` 被设置为 `true`，则当套接字的另一端发送 FIN 数据包时，服务器将仅在 [`socket.end()`] 被显式调用发回 FIN 数据包，直到此时连接为半封闭状态（不可读但仍然可写）。
有关详细信息，参阅 [`'end'`] 事件和 [RFC 1122][half-closed]（第 4.2.2.13 节）。

如果 `pauseOnConnect` 被设置为 `true`，则与每个传入连接关联的套接字会被暂停，并且不会从其句柄读取任何数据。
这允许在进程之间传递连接，而原始进程不会读取任何数据。
要从暂停的套接字开始读取数据，则调用 [`socket.resume()`]。

服务器可以是一个 TCP 服务器或 [IPC] 服务器，这取决于 [`listen()`][`server.listen()`] 监听什么。


以下是一个 TCP 回声服务器的示例，在 8124 端口上监听连接：

```js
const net = require('net');
const server = net.createServer((c) => {
  // 'connection' 监听器。
  console.log('客户端已连接');
  c.on('end', () => {
    console.log('客户端已断开连接');
  });
  c.write('你好\r\n');
  c.pipe(c);
});
server.on('error', (err) => {
  throw err;
});
server.listen(8124, () => {
  console.log('服务器已启动');
});
```

使用 `telnet` 测试：

```console
$ telnet localhost 8124
```

要想在 `/tmp/echo.sock` 上监听，则最后三行需改为：

```js
server.listen('/tmp/echo.sock', () => {
  console.log('服务器已启动');
});
```

使用 `nc` 连接到 UNIX 域套接字服务器：

```console
$ nc -U /tmp/echo.sock
```
