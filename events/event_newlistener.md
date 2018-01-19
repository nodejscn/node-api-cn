<!-- YAML
added: v0.1.26
-->

* `eventName` {any} 要监听的事件的名称
* `listener` {Function} 事件的句柄函数

`EventEmitter` 实例会在一个监听器被添加到其内部监听器数组之前触发自身的 `'newListener'` 事件。

注册了 `'newListener'` 事件的监听器会传入事件名与被添加的监听器的引用。

事实上，在添加监听器之前触发事件有一个微妙但重要的副作用：
在`'newListener'` 回调函数中, 一个监听器的名字如果和已有监听器名称相同, 则在被插入到EventEmitter实例的内部监听器数组时, 该监听器会被添加到其它同名监听器的前面。


```js
const myEmitter = new EventEmitter();
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

