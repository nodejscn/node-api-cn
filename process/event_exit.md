<!-- YAML
added: v0.1.7
-->

两种情况下 `'exit'` 事件会被触发：
* 显式调用 `process.exit()` 方法，使得 Node.js 进程即将结束；
* Node.js 事件循环数组中不再有额外的工作，使得 Node.js 进程即将结束。

在上述两种情况下，没有任何方法可以阻止事件循环的结束，一旦所有与 `'exit'` 事件绑定的监听器执行完成，Node.js 的进程会终止。

`'exit'` 事件监听器的回调函数，只有一个入参，这个参数的值可以是 [`process.exitCode`] 的属性值，或者是调用 [`process.exit()`] 方法时传入的 `exitCode` 值。

例如：

```js
process.on('exit', (code) => {
  console.log(`即将退出，退出码：${code}`);
});
```

`'exit'` 事件监听器的回调函数，只允许包含同步操作。所有监听器的回调函数被调用后，任何在事件循环数组中排队的工作都会被强制丢弃，然后 Nodje.js 进程会立即结束。
例如在下例中，定时器中的操作永远不会被执行（因为不是同步操作）。

```js
process.on('exit', (code) => {
  setTimeout(() => {
    console.log('该函数不会被执行');
  }, 0);
});
```
