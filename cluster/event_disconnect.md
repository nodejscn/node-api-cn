<!-- YAML
added: v0.7.7
-->

和`cluster.on('disconnect')`事件类似，不同之处在于特指这个工作进程。
```js
cluster.fork().on('disconnect', () => {
  // Worker has disconnected
});
```

