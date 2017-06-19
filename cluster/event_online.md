<!-- YAML
added: v0.7.0
-->

和`cluster.on('online')`事件类似，但针对特定的工作进程。

```js
cluster.fork().on('online', () => {
  // Worker is online
});
```

本事件不会在工作进程内部被触发。

