
`EventEmitter` 以注册的顺序同步地调用所有监听器。
这样可以确保事件的正确排序，并有助于避免竞态条件和逻辑错误。
当适当时，监听器函数可以使用 `setImmediate()` 和 `process.nextTick()` 方法切换到异步的操作模式：

```js
const myEmitter = new MyEmitter();
myEmitter.on('event', (a, b) => {
  setImmediate(() => {
    console.log('异步地发生');
  });
});
myEmitter.emit('event', 'a', 'b');
```

