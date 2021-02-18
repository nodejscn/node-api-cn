<!-- YAML
added: v0.11.12
-->

当 Node.js 清空其事件循环并且没有其他工作要调度时，则 `'beforeExit'` 事件会被触发。 
通常，当没有工作被调度时，则 Node.js 进程会退出，但是在 `'beforeExit'` 事件上注册的监听器可以进行异步的调用，从而使 Node.js 进程继续。

监听器回调函数被调用时会传入 [`process.exitCode`] 的值作为唯一的参数。

对于导致显式终止的情况（例如调用 [`process.exit()`] 或未捕获的异常），则不会触发 `'beforeExit'` 事件。

除非打算调度额外的工作，否则不应该使用 `'beforeExit'` 代替 `'exit'` 事件。

```js
process.on('beforeExit', (code) => {
  console.log('进程 beforeExit 事件的退出码: ', code);
});

process.on('exit', (code) => {
  console.log('进程 exit 事件的退出码: ', code);
});

console.log('此消息会最先显示');

// 打印:
// 此消息会最先显示
// 进程 beforeExit 事件的退出码: 0
// 进程 exit 事件的退出码: 0
```



