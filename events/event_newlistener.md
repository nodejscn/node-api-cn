<!-- YAML
added: v0.1.26
-->

* `eventName` {any} 要监听的事件的名称
* `listener` {Function} 事件的句柄函数

`EventEmitter` 实例会在一个监听器被添加到其内部监听器数组之前触发自身的 `'newListener'` 事件。

注册了 `'newListener'` 事件的监听器会传入事件名与被添加的监听器的引用。

事实上，在添加监听器之前触发事件有一个微妙但重要的副作用：
`'newListener'` 回调中任何额外的被注册到相同名称的监听器会在监听器被添加之前被插入 。


```js
const myEmitter = new MyEmitter();
// 只处理一次，所以不会无限循环
myEmitter.once('newListener', (event, listener) => {
  if (event === 'event') {
    // 在开头插入一个新的监听器
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

