<!-- YAML
added: v0.1.90
-->

如果在IP socket上监听,则返回绑定的ip地址, 地址族和操作系统报告的服务端口
在找到操作系统分配的地址时，找到指定的端口是有用的.返回一个有 `port`, `family`, 和 `address` 属性:
`{ port: 12346, family: 'IPv4', address: '127.0.0.1' }`的对象

对于在管道或UNIX域套接字上侦听的server,该名称将返回为字符串

例子:

```js
const server = net.createServer((socket) => {
  socket.end('goodbye\n');
}).on('error', (err) => {
  // handle errors here
  throw err;
});

// grab an arbitrary unused port.
server.listen(() => {
  console.log('opened server on', server.address());
});
```

只有到了 `'listening'` 事件被触发时候.才可以调用 `server.address()` 

