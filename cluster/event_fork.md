<!-- YAML
added: v0.7.0
-->

* `worker` {cluster.Worker}

当新的工作进程被衍生时，cluster 模块将会触发 `'fork'` 事件。
可以被用来记录工作进程活动，并产生一个自定义的超时。

```js
const timeouts = [];
function errorMsg() {
  console.error('连接出错');
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

