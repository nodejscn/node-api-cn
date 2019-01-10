<!-- YAML
added: v0.1.26
-->

* `eventName` {string|symbol} 事件的名称。
* `listener` {Function} 事件的句柄函数。

`EventEmitter` 实例在新的监听器被添加到其内部监听器数组之前，会触发自身的 `'newListener'` 事件。


在添加监听器之前触发 `'newListener'` 事件有一个副作用：
如果在回调中注册同名事件的监听器，则该监听器会被插入到正被添加的监听器前面。


```js
const myEmitter = new MyEmitter();
// 只处理一次，避免无限循环。
myEmitter.once('newListener', (event, listener) => {
  if (event === 'event') {
    // 在前面插入一个新的监听器。
    myEmitter.on('event', () => {
      console.log('B');
    });
  }
});
myEmitter.on('event', () => {
  console.log('A');
});
myEmitter.emit('event');
// 打印:
//   B
//   A
```

