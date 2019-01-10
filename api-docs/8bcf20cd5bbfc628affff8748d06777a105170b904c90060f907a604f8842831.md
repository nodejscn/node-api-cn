<!-- YAML
added: v6.0.0
-->

* {boolean}

当调用 `.kill()` 或者 `.disconnect()`方法时被设置，在这之前都是 `undefined`。

`worker.exitedAfterDisconnect`可以用于区分自发退出还是被动退出，主进程可以根据这个值决定是否重新衍生新的工作进程。

```js
cluster.on('exit', (worker, code, signal) => {
  if (worker.exitedAfterDisconnect === true) {
    console.log('Oh, it was just voluntary – no need to worry');
  }
});

// 关闭 worker
worker.kill();
```
