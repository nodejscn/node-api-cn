<!-- YAML
added: v0.1.26
-->

* `eventName` {string|symbol} 事件的名称。
* `listener` {Function} 事件的句柄函数。

`EventEmitter` 实例在新的监听器被添加到其内部监听器数组之前，会触发自身的 `'newListener'` 事件。

为 `'newListener'` 事件注册的监听器将传递事件名称和对要添加的监听器的引用。

在添加监听器之前触发事件的事实具有微妙但重要的副作用：在 `'newListener'` 回调中注册到相同 `name` 的任何其他监听器将插入到正在添加的监听器之前。


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

