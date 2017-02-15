
同样，`sendHandle` 参数可用于将一个 socket 句柄传给子进程。
以下例子衍生了两个子进程，分别用于处理 "normal" 连接或优先处理 "special" 连接：

```js
const normal = require('child_process').fork('child.js', ['normal']);
const special = require('child_process').fork('child.js', ['special']);

// 开启 server，并发送 socket 给子进程
const server = require('net').createServer();
server.on('connection', (socket) => {

  // 特殊优先级
  if (socket.remoteAddress === '74.125.127.100') {
    special.send('socket', socket);
    return;
  }
  // 普通优先级
  normal.send('socket', socket);
});
server.listen(1337);
```

`child.js` 会接收到一个 socket 句柄，并作为第二个参数传给事件回调函数：

```js
process.on('message', (m, socket) => {
  if (m === 'socket') {
    socket.end(`请求被 ${process.argv[2]} 优先级处理`);
  }
});
```

一旦一个 socket 已被传给了子进程，则父进程不再能够跟踪 socket 何时被销毁。
为了表明这个，`.connections` 属性会变成 `null`。
当发生这种情况时，建议不要使用 `.maxConnections`。

注意，该函数内部使用 [`JSON.stringify()`] 序列化 `message`。

