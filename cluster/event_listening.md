<!-- YAML
added: v0.7.0
-->

* `address` {Object}

和`cluster.on('listening')`事件类似，但针对特定的工作进程。

```js
cluster.fork().on('listening', (address) => {
  // Worker is listening
});
```

本事件不会在工作进程内触发。
