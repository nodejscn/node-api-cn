<!-- YAML
added: v0.1.99
-->

* `port` {number} - 整数，可选的
* `address` {string}, 可选的
* `callback` {Function} - (没有参数)，可选的。当绑定完成时会被调用。

对于 UDP socket，该方法会令`dgram.Socket`在指定的`port`和可选的`address`上监听数据包信息。若`port`未指定或为 `0`，操作系统会尝试绑定一个随机的端口。若`address`未指定，操作系统会尝试在所有地址上监听。绑定完成时会触发一个`'listening'`事件，并会调用`callback`方法。

注意，同时监听`'listening'`事件和在`socket.bind()`方法中传入`callback`参数并不会带来坏处，但也不是很有用。

一个被绑定的数据包 socket 会令 Node.js 进程保持运行以接收数据包信息。

若绑定失败，一个`'error'`事件会被触发。在极少数的情况下（例如尝试绑定一个已关闭的 socket），一个 [`Error`][] 会被抛出。

一个监听 41234 端口的 UDP 服务器的例子：

```js
const dgram = require('dgram');
const server = dgram.createSocket('udp4');

server.on('error', (err) => {
  console.log(`服务器异常：\n${err.stack}`);
  server.close();
});

server.on('message', (msg, rinfo) => {
  console.log(`服务器收到：${msg} 来自 ${rinfo.address}:${rinfo.port}`);
});

server.on('listening', () => {
  const address = server.address();
  console.log(`服务器监听 ${address.address}:${address.port}`);
});

server.bind(41234);
// 服务器监听 0.0.0.0:41234
```

