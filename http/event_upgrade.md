<!-- YAML
added: v0.1.94
-->

* `response` {http.IncomingMessage}
* `socket` {stream.Duplex}
* `head` {Buffer}

每次服务器响应升级请求时发出。
如果未监听此事件且响应状态码为 `101 Switching Protocols`，则接收升级响应头的客户端将关闭其连接。

此事件保证传入 {net.Socket} 类（{stream.Duplex} 的子类）的实例，除非用户指定了 {net.Socket} 以外的套接字类型。

客户端服务器对，演示如何监听 `'upgrade'` 事件。

```js
const http = require('http');

// 创建 HTTP 服务器。
const server = http.createServer((req, res) => {
  res.writeHead(200, { 'Content-Type': 'text/plain' });
  res.end('响应内容');
});
server.on('upgrade', (req, socket, head) => {
  socket.write('HTTP/1.1 101 Web Socket Protocol Handshake\r\n' +
               'Upgrade: WebSocket\r\n' +
               'Connection: Upgrade\r\n' +
               '\r\n');

  socket.pipe(socket); // 响应回去。
});

// 服务器正在运行。
server.listen(1337, '127.0.0.1', () => {

  // 发送请求。
  const options = {
    port: 1337,
    host: '127.0.0.1',
    headers: {
      'Connection': 'Upgrade',
      'Upgrade': 'websocket'
    }
  };

  const req = http.request(options);
  req.end();

  req.on('upgrade', (res, socket, upgradeHead) => {
    console.log('接收到响应');
    socket.end();
    process.exit(0);
  });
});
```

