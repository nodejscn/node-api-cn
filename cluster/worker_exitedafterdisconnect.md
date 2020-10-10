<!-- YAML
added: v6.0.0
-->

* {boolean}

如果工作进程由于 `.kill()` 或 `.disconnect()` 而退出，则此属性为 `true`。 
如果工作进程以任何其他方式退出，则为 `false`。 
如果工作进程尚未退出，则为 `undefined`。

[`worker.exitedAfterDisconnect`] 可以用于区分自发退出还是被动退出，主进程可以根据这个值决定是否重新衍生工作进程。


```js
cluster.on('exit', (worker, code, signal) => {
  if (worker.exitedAfterDisconnect === true) {
    console.log('这是自发退出，无需担心');
  }
});

// 杀死工作进程。
worker.kill();
```

