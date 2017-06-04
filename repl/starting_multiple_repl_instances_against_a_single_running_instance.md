
可以在一个 Node.js 实例中创建并运行多个 REPL 实例，它们共享一个 `global` 对象但有独立的 I/O 接口。

例子，在 `stdin`、Unix socket、和 TCP socket 上分别提供了独立的 REPL：

```js
const net = require('net');
const repl = require('repl');
let connections = 0;

repl.start({
  prompt: 'Node.js 使用 stdin> ',
  input: process.stdin,
  output: process.stdout
});

net.createServer((socket) => {
  connections += 1;
  repl.start({
    prompt: 'Node.js 使用 Unix socket> ',
    input: socket,
    output: socket
  }).on('exit', () => {
    socket.end();
  });
}).listen('/tmp/node-repl-sock');

net.createServer((socket) => {
  connections += 1;
  repl.start({
    prompt: 'Node.js 使用 TCP socket> ',
    input: socket,
    output: socket
  }).on('exit', () => {
    socket.end();
  });
}).listen(5001);
```

从命令行运行这个应用会在 stdin 上启动一个 REPL。
其他 REPL 客户端可以通过 Unix socket 或 TCP socket 进行连接。
例如，可以使用 `telnet` 连接到 TCP socket，使用 `socat` 连接到 Unix socket 或 TCP socket。

通过从一个基于 Unix socket 的服务器（而不是 stdin）启动一个 REPL，可以连接到一个长期运行的 Node.js 进程而无需重启它。

例子，在一个 `net.Server` 实例和一个 `net.Socket` 实例上运行一个全特性的（`terminal`）REPL，详见：https://gist.github.com/2209310

例子，在 [curl(1)][] 上运行一个 REPL 实例，详见：https://gist.github.com/2053342

