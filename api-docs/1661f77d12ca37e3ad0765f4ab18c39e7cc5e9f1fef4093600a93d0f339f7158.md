<!-- YAML
added: v0.1.18
-->

当未捕获的 JavaScript 异常一直冒泡回到事件循环时，会触发 `'uncaughtException'` 事件。 
默认情况下，Node.js 通过将堆栈跟踪打印到 `stderr` 并使用退出码 `1` 来处理此类异常，从而覆盖任何先前设置的 [`process.exitCode`]。 
为 `'uncaughtException'` 事件添加处理程序会覆盖此默认行为。 
或者，更改 `'uncaughtException'` 处理程序中的 [`process.exitCode`]，这将导致进程退出并提供退出码。 
否则，在存在这样的处理程序的情况下，进程将以 `0` 退出。

调用监听器函数时，将 `Error` 对象作为唯一参数传入。


```js
process.on('uncaughtException', (err) => {
  fs.writeSync(1, `捕获的异常：${err}\n`);
});

setTimeout(() => {
  console.log('这里仍然会运行');
}, 500);

// 故意引起异常，但不要捕获它。
nonexistentFunc();
console.log('这里不会运行');
```

