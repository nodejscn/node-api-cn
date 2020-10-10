<!-- YAML
added: v0.7.0
-->

类似于 `cluster.on('online')` 事件，但特定于此工作进程。 

```js
cluster.fork().on('online', () => {
  // 工作进程已上线。
});
```

此事件不会在工作进程中触发。

