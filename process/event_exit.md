<!-- YAML
added: v0.1.7
-->

* `code` {integer} 进程的退出码，可能是 [`process.exitCode`] 或传入 [`process.exit()`] 的 `exitCode`。

当 Node.js 进程因以下原因之一即将退出时会触发 `'exit'` 事件：

* 调用 `process.exit()`；
* Node.js 事件循环不再有额外的工作。

没有任何方法可以阻止事件循环的结束，当所有的 `'exit'` 事件监听器执行完成时，Node.js 进程就会终止。

```js
process.on('exit', (code) => {
  console.log(`退出码: ${code}`);
});
```

`'exit'` 事件监听器的回调函数只允许同步操作。
`'exit'` 事件监听器被调用后，Nodje.js 进程会立即退出，事件循环排队中的工作都会被丢弃。
以下例子中，定时器中的操作不会被执行：

```js
process.on('exit', (code) => {
  setTimeout(() => {
    console.log('该函数不会被执行');
  }, 0);
});
```

