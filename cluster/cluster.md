
<!--introduced_in=v0.10.0-->

> 稳定性: 2 - 稳定的

Node.js在单个线程中运行单个实例。
用户(开发者)为了使用现在的多核系统，有时候,用户(开发者)会用一串Node.js进程去处理负载任务。

`cluster` 模块允许简单容易的创建共享服务器端口的子进程。

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
现在运行 `Node.js` 将会在工作进程(指代子进程)之间共享8000端口

```txt
$ node server.js
主进程 3596 正在运行
工作进程 4324 已启动
工作进程 4520 已启动
工作进程 6056 已启动
工作进程 5644 已启动
```
请注意,在Windows中,还不能在工作进程中设置管道(Pipe)服务器。

