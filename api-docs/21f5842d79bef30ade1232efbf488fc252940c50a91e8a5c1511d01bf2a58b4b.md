<!-- YAML
added: v0.7.9
-->

* `worker` {cluster.Worker}
* `code` {number} 正常退出时的退出代码。
* `signal` {string} 导致进程被杀死的信号名称 (例如 `'SIGHUP'`)。

当任何一个工作进程关闭的时候，cluster 模块都将会触发 `'exit'` 事件。

这可以用于重启工作进程（通过再次调用 `.fork()`）。

```js
cluster.on('exit', (worker, code, signal) => {
  console.log('工作进程 %d 关闭 (%s). 重启中...',
              worker.process.pid, signal || code);
  cluster.fork();
});
```

参阅 [`child_process` event: `'exit'`]。

