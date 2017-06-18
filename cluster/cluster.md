
> 稳定性: 2 - 稳定的

一个单一的 Node.js 实例运行在一个单独的线程上。
为了利用多核系统，用户有时会想启动一个 Node.js 进程的集群去处理负载。

`cluster` 模块可以轻松地创建一些共享服务器端口的子进程。

```js
const cluster = require('cluster');
const http = require('http');
const numCPUs = require('os').cpus().length;

if (cluster.isMaster) {
  console.log(`主进程 ${process.pid} 正在运行`);

  // 衍生工作进程。
  for (let i = 0; i < numCPUs; i++) {
    cluster.fork();
  }

  cluster.on('exit', (worker, code, signal) => {
    console.log(`工作进程 ${worker.process.pid} 已退出`);
  });
} else {
  // 工作进程可以共享任何 TCP 连接。
  // 在本例子中，共享的是一个 HTTP 服务器。
  http.createServer((req, res) => {
    res.writeHead(200);
    res.end('你好世界\n');
  }).listen(8000);

  console.log(`工作进程 ${process.pid} 已启动`);
}
```

运行 Node.js 则工作进程就会共享 8000 端口：

```txt
$ node server.js
主进程 3596 正在运行
工作进程 4324 已启动
工作进程 4520 已启动
工作进程 6056 已启动
工作进程 5644 已启动
```

注意，在 Windows 上还不能在一个工作进程中建立一个命名的管道服务器。

