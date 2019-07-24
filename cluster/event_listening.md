<!-- YAML
added: v0.7.0
-->

* `address` {Object}

类似于 `cluster.on('listening')` 事件，但特定于此工作进程。 

```js
cluster.fork().on('listening', (address) => {
  // 工作进程正在监听。
});
```

此事件不会在工作进程中触发。

