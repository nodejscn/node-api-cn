
当使用 `eventEmitter.on()` 方法注册监听器时，监听器会在每次触发命名事件时被调用。

```js
const myEmitter = new MyEmitter();
let m = 0;
myEmitter.on('event', () => {
  console.log(++m);
});
myEmitter.emit('event');
// 打印: 1
myEmitter.emit('event');
// 打印: 2
```

使用 `eventEmitter.once()` 方法时可以注册一个对于特定事件最多被调用一次的监听器。
当事件被触发时，监听器会被注销，然后再调用。


```js
const myEmitter = new MyEmitter();
let m = 0;
myEmitter.once('event', () => {
  console.log(++m);
});
myEmitter.emit('event');
// 打印: 1
myEmitter.emit('event');
// 忽略
```

