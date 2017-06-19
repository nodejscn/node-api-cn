<!-- YAML
added: v0.7.0
-->

* `worker` {cluster.Worker}

当新的工作进程被fork时，cluster模块将触发`'fork'`事件。
可以被用来记录工作进程活动，产生一个自定义的timeout。

```js
const timeouts = [];
function errorMsg() {
  console.error('Something must be wrong with the connection ...');
}

cluster.on('fork', (worker) => {
  timeouts[worker.id] = setTimeout(errorMsg, 2000);
});
cluster.on('listening', (worker, address) => {
  clearTimeout(timeouts[worker.id]);
});
cluster.on('exit', (worker, code, signal) => {
  clearTimeout(timeouts[worker.id]);
  errorMsg();
});
```

