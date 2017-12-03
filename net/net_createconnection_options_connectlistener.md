<!-- YAML
added: v0.1.90
-->

* `options` {Object} 必须。调用 [`new net.Socket([options])`][`new net.Socket(options)`] 和 [`socket.connect(options[, connectListener])`][`socket.connect(options)`] 方法都会传入。
* `connectListener` {Function} [`net.createConnection()`][] 方法的通用参数。如果制定了，将被添加为返回 socket 上的 [`'connect'`][] 事件上的监听器。
* Returns: {net.Socket} 新创建的 socket，用于开始连接。

可选的选项，查看 [`new net.Socket([options])`][`new net.Socket(options)`] 和 [`socket.connect(options[, connectListener])`][`socket.connect(options)`]。

附加的选项：

* `timeout` {number} 如果设置，将会用来在 socket 创建之后连接开始之前调用 [`socket.setTimeout(timeout)`][]。

虾米是在 [`net.createServer()`][] 章节描述的 server 的客户端示例：

```js
const net = require('net');
const client = net.createConnection({ port: 8124 }, () => {
  //'connect' listener
  console.log('connected to server!');
  client.write('world!\r\n');
});
client.on('data', (data) => {
  console.log(data.toString());
  client.end();
});
client.on('end', () => {
  console.log('disconnected from server');
});
```

如果要连接到 `/tmp/echo.sock`，第二行只需要改为：

```js
const client = net.createConnection({ path: '/tmp/echo.sock' });
```

