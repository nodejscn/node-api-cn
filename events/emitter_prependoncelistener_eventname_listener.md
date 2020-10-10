<!-- YAML
added: v6.0.0
-->

* `eventName` {string|symbol} 事件名称。
* `listener` {Function} 回调函数。
* 返回: {EventEmitter}

添加单次监听器 `listener` 到名为 `eventName` 的事件的监听器数组的开头。
当 `eventName` 事件下次触发时，监听器会先被移除，然后再调用。

```js
server.prependOnceListener('connection', (stream) => {
  console.log('第一次调用');
});
```

返回对 `EventEmitter` 的引用，以便可以链式调用。

