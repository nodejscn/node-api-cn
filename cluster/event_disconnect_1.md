<!-- YAML
added: v0.7.9
-->

* `worker` {cluster.Worker}

在工作进程的IPC管道被断开后触发本事件。可能导致事件触发的原因包括：工作进程优雅地退出、被kill或手动断开连接（如调用worker.disconnect()）。

`'disconnect'` 和 `'exit'`事件之间可能存在延迟。这些事件可以用来检测进程是否在清理过程中被卡住，或是否存在长时间运行的连接。

```js
cluster.on('disconnect', (worker) => {
  console.log(`The worker #${worker.id} has disconnected`);
});
```

