
当 `EventEmitter` 实例中发生错误时，会触发一个 `'error'` 事件。
这在 Node.js 中是特殊情况。

如果 `EventEmitter` 没有为 `'error'` 事件注册至少一个监听器，则当 `'error'` 事件触发时，会抛出错误、打印堆栈跟踪、且退出 Node.js 进程。

```js
const myEmitter = new MyEmitter();
myEmitter.emit('error', new Error('whoops!'));
// 抛出错误，并使 Node.js 奔溃
```

为了防止 Node.js 进程崩溃，可以在 [`process` 对象的 `uncaughtException` 事件]上注册监听器，或使用 [`domain`] 模块。
（注意，`domain` 模块已被废弃。）

```js
const myEmitter = new MyEmitter();

process.on('uncaughtException', (err) => {
  console.error('有错误');
});

myEmitter.emit('error', new Error('whoops!'));
// 打印: 有错误
```

作为最佳实践，应该始终为 `'error'` 事件注册监听器。

```js
const myEmitter = new MyEmitter();
myEmitter.on('error', (err) => {
  console.error('有错误');
});
myEmitter.emit('error', new Error('whoops!'));
// 打印: 有错误
```

