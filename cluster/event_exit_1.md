<!-- YAML
added: v0.7.9
-->

* `worker` {cluster.Worker}
* `code` {number} 正常退出情况下，是退出代码.
* `signal` {string} 导致进程被kill的信号名称 (例如 `'SIGHUP'`)

当任何一个工作进程关闭的时候，cluster模块都将触发`'exit'`事件。

可以被用来重启工作进程（）通过调用`.fork()`）。

```js
cluster.on('exit', (worker, code, signal) => {
  console.log('worker %d died (%s). restarting...',
              worker.process.pid, signal || code);
  cluster.fork();
});
```

详见： [child_process event: 'exit'][]。

