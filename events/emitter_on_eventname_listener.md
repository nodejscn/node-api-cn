<!-- YAML
added: v0.1.101
-->

* `eventName` {any} 事件名
* `listener` {Function} 回调函数

添加 `listener` 函数到名为 `eventName` 的事件的监听器数组的末尾。
不会检查 `listener` 是否已被添加。
多次调用并传入相同的 `eventName` 和 `listener` 会导致 `listener` 被添加与调用多次。


```js
server.on('connection', (stream) => {
  console.log('有连接！');
});
```

返回一个 `EventEmitter` 引用，可以链式调用。

默认情况下，事件监听器会按照添加的顺序依次调用。
`emitter.prependListener()` 方法可用于将事件监听器添加到监听器数组的开头。

```js
const myEE = new EventEmitter();
myEE.on('foo', () => console.log('a'));
myEE.prependListener('foo', () => console.log('b'));
myEE.emit('foo');
// 打印:
//   b
//   a
```

