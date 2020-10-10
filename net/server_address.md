<!-- YAML
added: v0.1.90
-->

* 返回: {Object|string|null}

如果在 IP socket 上监听，则返回操作系统报告的绑定的 `address`、地址 `family` 名称、以及服务器 `port`（用于查找在获取操作系统分配的地址时分配的端口）：`{ port: 12346, family: 'IPv4', address: '127.0.0.1' }`。

对于在管道或 Unix 域套接字上监听的 server，该名称将返回为字符串。

```js
const server = net.createServer((socket) => {
  socket.end('再见\n');
}).on('error', (err) => {
  // 处理错误
  throw err;
});

// 获取任意未使用的端口。
server.listen(() => {
  console.log('打开服务器', server.address());
});
```

在 `'listening'` 事件被触发之前、或在调用 `server.close()` 之后，`server.address()` 返回 `null`。

