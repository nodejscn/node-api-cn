<!-- YAML
added: v0.3.0
-->

* `eventName` {any} 事件名
* `listener` {Function} 回调函数

添加一个单次 `listener` 函数到名为 `eventName` 的事件。
下次触发 `eventName` 事件时，监听器会被移除，然后调用。

```js
server.once('connection', (stream) => {
  console.log('首次调用！');
});
```

返回一个 `EventEmitter` 引用，可以链式调用。

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

