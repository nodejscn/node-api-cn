<!-- YAML
added: v6.0.0
-->

* `eventName` {any} 事件名
* `listener` {Function} 回调函数

添加 `listener` 函数到名为 `eventName` 的事件的监听器数组的开头。
不会检查 `listener` 是否已被添加。
多次调用并传入相同的 `eventName` 和 `listener` 会导致 `listener` 被添加与调用多次。

```js
server.prependListener('connection', (stream) => {
  console.log('有连接！');
});
```

返回一个 `EventEmitter` 引用，可以链式调用。

