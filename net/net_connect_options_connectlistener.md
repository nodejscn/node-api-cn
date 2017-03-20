<!-- YAML
added: v0.7.0
-->

一个生产器函数，将返回一个新的 [`net.Socket`][] 并且自动的根据所提供的`options` 参数进行连接。

options参数将被传递到[`net.Socket`][]构造函数和[`socket.connect`][]方法两个地方。

`connectListener`参数将一次被用作监听器来监听[`'connect'`][]事件。

下面有一个例子来阐述之前描述过的响应服务器的客户端的用法

```js
const net = require('net');
const client = net.connect({port: 8124}, () => {
  // 'connect' listener
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

为了连接`/tmp/echo.sock`的socket，第二行应改为

```js
const client = net.connect({path: '/tmp/echo.sock'});
```

