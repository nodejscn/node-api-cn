<!-- YAML
added: v0.7.7
-->
 
类似于 `cluster.on('disconnect')` 事件，但特定于此工作进程。 
 
```js
cluster.fork().on('disconnect', () => {
  // 工作进程已断开连接。
});
```

