<!-- YAML
added: v0.1.26
changes:
  - version: v7.0.0
    pr-url: https://github.com/nodejs/node/pull/6881
    description: For listeners attached using `.once()` this returns the
                 original listeners instead of wrapper functions now.
-->
* `eventName` {string|symbol}
* 返回: {Function[]}

返回名为 `eventName` 的事件的监听器数组的副本。

```js
server.on('connection', (stream) => {
  console.log('有连接');
});
console.log(util.inspect(server.listeners('connection')));
// 打印: [ [Function] ]
```

