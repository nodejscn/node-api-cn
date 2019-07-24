<!-- YAML
added: v0.11.14
-->

当工作进程被终止时（包括自动退出或被发送信号），这个方法返回 `true`。
否则，返回 `false`。

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

  cluster.on('fork', (worker) => {
    console.log('工作进程已关闭:', worker.isDead());
  });

  cluster.on('exit', (worker, code, signal) => {
    console.log('工作进程已关闭:', worker.isDead());
  });
} else {
  // 工作进程可以共享任何 TCP 连接。在这种情况下，它是一个 HTTP 服务器。
  http.createServer((req, res) => {
    res.writeHead(200);
    res.end(`当前进程\n ${process.pid}`);
    process.kill(process.pid);
  }).listen(8000);
}
```

