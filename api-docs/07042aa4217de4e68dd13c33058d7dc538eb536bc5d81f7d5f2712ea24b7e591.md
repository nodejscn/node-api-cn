<!-- YAML
added: v0.1.7
-->

* `code` {integer}

当 Node.js 进程因以下原因之一即将退出时，则会触发 `'exit'` 事件：

* 显式调用 `process.exit()` 方法；
* Node.js 事件循环不再需要执行任何其他工作。

此时无法阻止退出事件循环，并且一旦所有 `'exit'` 事件的监听器都已完成运行时，Node.js 进程将终止。

使用 [`process.exitCode`] 属性指定的退出码或传给 [`process.exit()`] 方法的 `exitCode` 参数调用监听器回调函数。

```js
process.on('exit', (code) => {
  console.log(`退出码: ${code}`);
});
```

监听器函数必须只执行同步操作。
在调用 `'exit'` 事件监听器之后，Node.js 进程将立即退出，从而导致在事件循环中仍排队的任何其他工作被放弃。
例如，在以下示例中，定时器中的操作不会发生：

```js
process.on('exit', (code) => {
  setTimeout(() => {
    console.log('此处不会运行');
  }, 0);
});
```

