
> Stability: 2 - Stable

A single instance of Node.js runs in a single thread. To take advantage of
multi-core systems the user will sometimes want to launch a cluster of Node.js
processes to handle the load.

The cluster module allows you to easily create child processes that
all share server ports.

```js
const cluster = require('cluster');
const http = require('http');
const numCPUs = require('os').cpus().length;

if (cluster.isMaster) {
  // Fork workers.
  for (var i = 0; i < numCPUs; i++) {
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
}
```

Running Node.js will now share port 8000 between the workers:

```txt
$ NODE_DEBUG=cluster node server.js
23521,Master Worker 23524 online
23521,Master Worker 23526 online
23521,Master Worker 23523 online
23521,Master Worker 23528 online
```

Please note that on Windows, it is not yet possible to set up a named pipe
server in a worker.

