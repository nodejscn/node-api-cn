<!-- YAML
added: v0.7.0
-->

* {Object}

当前工作进程对象的引用，对于主进程则无效。

```js
const cluster = require('cluster');

if (cluster.isMaster) {
  console.log('I am master');
  cluster.fork();
  cluster.fork();
} else if (cluster.isWorker) {
  console.log(`I am worker #${cluster.worker.id}`);
}
```

