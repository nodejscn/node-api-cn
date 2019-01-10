<!-- YAML
added: v0.11.2
-->

* `code` {number} 若正常退出，表示退出代码.
* `signal` {string} 引发进程被kill的信号名称（如`'SIGHUP'`）.

和`cluster.on('exit')`事件类似，但针对特定的工作进程。

```js
const worker = cluster.fork();
worker.on('exit', (code, signal) => {
  if (signal) {
    console.log(`worker was killed by signal: ${signal}`);
  } else if (code !== 0) {
    console.log(`worker exited with error code: ${code}`);
  } else {
    console.log('worker success!');
  }
});
```

