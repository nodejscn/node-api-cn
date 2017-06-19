<!-- YAML
added: v0.7.0
deprecated: v6.0.0
changes:
  - version: v7.0.0
    pr-url: https://github.com/nodejs/node/pull/3747
    description: Accessing this property will now emit a deprecation warning.
-->

> Stability: 0 - Deprecated: Use [`worker.exitedAfterDisconnect`][] instead.

和 [`worker.exitedAfterDisconnect`][] 等价.

调用`.kill()` 或`.disconnect()`被设置，否则一直是 `undefined`。

 `worker.suicide`用于区分自发退出或被动退出，主进程可根据这个值来决定是否重新衍生新的工作进程。

```js
cluster.on('exit', (worker, code, signal) => {
  if (worker.suicide === true) {
    console.log('Oh, it was just voluntary – no need to worry');
  }
});

// kill worker
worker.kill();
```

这个API只是为了向后兼容，未来会删除。

