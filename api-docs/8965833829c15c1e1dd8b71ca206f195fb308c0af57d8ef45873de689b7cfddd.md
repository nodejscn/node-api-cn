<!-- YAML
added: v0.11.2
-->

* `code` {number} 正常退出时的退出代码。
* `signal` {string} 导致进程被杀死的信号名称 (例如 `'SIGHUP'`)。

类似于 `cluster.on('exit')` 事件，但特定于此工作进程。 

```js
const worker = cluster.fork();
worker.on('exit', (code, signal) => {
  if (signal) {
    console.log(`工作进程已被信号 ${signal} 杀死`);
  } else if (code !== 0) {
    console.log(`工作进程退出，退出码: ${code}`);
  } else {
    console.log('工作进程成功退出');
  }
});
```

