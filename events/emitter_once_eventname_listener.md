<!-- YAML
added: v0.3.0
-->

* `eventName` {string|symbol} 事件名称。
* `listener` {Function} 回调函数。
* 返回: {EventEmitter}

添加单次监听器 `listener` 到名为 `eventName` 的事件。
当 `eventName` 事件下次触发时，监听器会先被移除，然后再调用。

```js
server.once('connection', (stream) => {
  console.log('第一次调用');
});
```

返回对 `EventEmitter` 的引用，以便可以链式调用。

默认情况下，事件监听器会按照添加的顺序依次调用。
`emitter.prependOnceListener()` 方法可用于将事件监听器添加到监听器数组的开头。

```js
const myEE = new EventEmitter();
myEE.once('foo', () => console.log('a'));
myEE.prependOnceListener('foo', () => console.log('b'));
myEE.emit('foo');
// 打印:
//   b
//   a
```

