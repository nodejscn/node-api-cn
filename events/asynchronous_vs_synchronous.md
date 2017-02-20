
`EventListener` 会按照监听器注册的顺序同步地调用所有监听器。
所以需要确保事件的正确排序且避免竞争条件或逻辑错误。
监听器函数可以使用 `setImmediate()` 或 `process.nextTick()` 方法切换到异步操作模式：

```js
const myEmitter = new MyEmitter();
myEmitter.on('event', (a, b) => {
  setImmediate(() => {
    console.log('这个是异步发生的');
  });
});
myEmitter.emit('event', 'a', 'b');
```

