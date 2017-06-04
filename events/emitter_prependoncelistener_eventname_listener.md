<!-- YAML
added: v6.0.0
-->

* `eventName` {any} 事件名
* `listener` {Function} 回调函数

添加一个单次 `listener` 函数到名为 `eventName` 的事件的监听器数组的开头。
下次触发 `eventName` 事件时，监听器会被移除，然后调用。

```js
server.prependOnceListener('connection', (stream) => {
  console.log('首次调用！');
});
```

返回一个 `EventEmitter` 引用，可以链式调用。

