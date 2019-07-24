<!-- YAML
added: v6.0.0
-->

* {boolean}

当调用 `.kill()` 或者 `.disconnect()` 方法时被设置，在这之前都是 `undefined`。

[`worker.exitedAfterDisconnect`] 可以用于区分自发退出还是被动退出，主进程可以根据这个值决定是否重新衍生新的工作进程。

```js
cluster.on('exit', (worker, code, signal) => {
  if (worker.exitedAfterDisconnect === true) {
    console.log('这是自发退出，无需担心。');
  }
});

// 杀死工作进程。
worker.kill();
```

