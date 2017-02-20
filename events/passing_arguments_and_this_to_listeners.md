
`eventEmitter.emit()` 方法允许将任意参数传给监听器函数。
当一个普通的监听器函数被 `EventEmitter` 调用时，标准的 `this` 关键词会被设置指向监听器所附加的 `EventEmitter`。

```js
const myEmitter = new MyEmitter();
myEmitter.on('event', function(a, b) {
  console.log(a, b, this);
  // 打印:
  //   a b MyEmitter {
  //     domain: null,
  //     _events: { event: [Function] },
  //     _eventsCount: 1,
  //     _maxListeners: undefined }
});
myEmitter.emit('event', 'a', 'b');
```

也可以使用 ES6 的箭头函数作为监听器。但是这样 `this` 关键词就不再指向 `EventEmitter` 实例：

```js
const myEmitter = new MyEmitter();
myEmitter.on('event', (a, b) => {
  console.log(a, b, this);
  // 打印: a b {}
});
myEmitter.emit('event', 'a', 'b');
```

