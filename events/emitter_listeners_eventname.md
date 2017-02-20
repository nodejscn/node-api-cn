<!-- YAML
added: v0.1.26
-->

返回名为 `eventName` 的事件的监听器数组的副本。

```js
server.on('connection', (stream) => {
  console.log('someone connected!');
});
console.log(util.inspect(server.listeners('connection')));
// 打印: [ [Function] ]
```

