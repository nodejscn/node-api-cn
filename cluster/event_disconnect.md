<!-- YAML
added: v0.7.7
-->
 
虽然与 `cluster.on('disconnect')`事件 是相似的,但是这个进程又有其他特征。 
 
```js
cluster.fork().on('disconnect', () => {
  // Worker has disconnected
});
```

