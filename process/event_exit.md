<!-- YAML
added: v0.1.7
-->

* `code` {integer}

当 Node.js 进程因以下原因之一即将退出时，则会触发 `'exit'` 事件：

* `process.exit()` 方法被显式地调用；
* Node.js 事件循环不再需要执行任何其他的工作。

此时无法阻止事件循环的退出，并且一旦所有的 `'exit'` 事件的监听器都已完成运行，则 Node.js 进程就会终止。

监听器回调函数被调用时会传入退出码（由 [`process.exitCode`] 属性指定，或是传给 [`process.exit()`] 方法的 `exitCode` 参数）。

```js
process.on('exit', (code) => {
  console.log(`即将退出，退出码: ${code}`);
});
```

监听器函数必须只执行同步的操作。
在调用 `'exit'` 事件监听器之后，Node.js 进程会立即退出，从而使仍在事件循环中排队的任何其他的工作都被放弃。
例如，在以下示例中，定时器中的操作不会发生：

```js
process.on('exit', (code) => {
  setTimeout(() => {
    console.log('此处不会运行');
  }, 0);
});
```

