<!-- YAML
added: v0.7.0
-->

* `worker` {cluster.Worker}

当衍生一个新的工作进程后，工作进程应当响应一个上线消息。
当主进程收到上线消息后将会触发此事件。
`'fork'` 事件和 `'online'` 事件的区别在于，当主进程衍生工作进程时触发 `'fork'`，当工作进程运行时触发 `'online'`。

```js
cluster.on('online', (worker) => {
  console.log('工作进程被衍生后响应');
});
```

