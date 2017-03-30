
> 稳定性: 2 - 稳定的

Node.js的一个实例运行在一个单独的线程上。用多核系统的用户有时会想扩展一个Node.js的集群，去处理负载。

cluster模块可以让您轻松创建所有共享服务器端口的子进程。

```js
const cluster = require('cluster');
const http = require('http');
const numCPUs = require('os').cpus().length;

if (cluster.isMaster) {
  console.log(`Master ${process.pid} is running`);

  // Fork workers.
  for (let i = 0; i < numCPUs; i++) {
    cluster.fork();
  }

  cluster.on('exit', (worker, code, signal) => {
    console.log(`worker ${worker.process.pid} died`);
  });
} else {
  // Workers can share any TCP connection
  // In this case it is an HTTP server
  http.createServer((req, res) => {
    res.writeHead(200);
    res.end('hello world\n');
  }).listen(8000);

  console.log(`Worker ${process.pid} started`);
}
```

运行Node.js就能看到在8000端口下的所有进程：

```txt
$ node server.js
Master 3596 is running
Worker 4324 started
Worker 4520 started
Worker 6056 started
Worker 5644 started
```

请注意，在Windows上，还不能建立一个命名管道。
