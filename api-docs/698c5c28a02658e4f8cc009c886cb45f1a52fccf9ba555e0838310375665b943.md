
`EventEmitter` 会按照监听器注册的顺序同步地调用所有监听器。
所以必须确保事件的排序正确，且避免竞态条件。
可以使用 `setImmediate()` 或 `process.nextTick()` 切换到异步模式：

```js
const myEmitter = new MyEmitter();
myEmitter.on('event', (a, b) => {
  setImmediate(() => {
    console.log('异步进行');
  });
});
myEmitter.emit('event', 'a', 'b');
```

