
类似地，`sendHandle` 参数可用于将 socket 的句柄传给子进程。
以下示例衍生了两个子进程，分别用于处理 "normal" 连接或优先处理 "special" 连接：

```js
const { fork } = require('child_process');
const normal = fork('subprocess.js', ['normal']);
const special = fork('subprocess.js', ['special']);

// 开启 server，并发送 socket 给子进程。
// 使用 `pauseOnConnect` 防止 socket 在被发送到子进程之前被读取。
const server = require('net').createServer({ pauseOnConnect: true });
server.on('connection', (socket) => {

  // 特殊优先级。
  if (socket.remoteAddress === '74.125.127.100') {
    special.send('socket', socket);
    return;
  }
  // 普通优先级。
  normal.send('socket', socket);
});
server.listen(1337);
```

`subprocess.js` 会接收该 socket 句柄作为传给事件回调函数的第二个参数：

```js
process.on('message', (m, socket) => {
  if (m === 'socket') {
    if (socket) {
      // 检查客户端 socket 是否存在。
      // socket 在被发送与被子进程接收这段时间内可被关闭。
      socket.end(`请求使用 ${process.argv[2]} 优先级处理`);
    }
  }
});
```

一旦一个 socket 已被传给了子进程，则父进程不再能够跟踪 socket 何时被销毁。
为了表明这个，`.connections` 属性会变成 `null`。
当发生这种情况时，建议不要使用 `.maxConnections`。

建议在子进程中的任何 `'message'` 句柄都需要验证 `socket` 是否存在，因为连接可能会在它发送给子进程的这段时间内被关闭。

