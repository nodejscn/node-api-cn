<!-- YAML
added: v0.7.5
-->

每当 `input` 流接收到一个 `<ctrl>-Z` 输入（通常被称为 `SIGTSTP`）时，触发 `'SIGTSTP'` 事件。
当 `input` 流接收到一个 `SIGTSTP` 时，如果没有注册 `'SIGTSTP'` 事件监听器，则 Node.js 进程会被发送到后台。

当程序使用 fg(1p) 恢复时，`'pause'` 和 `SIGCONT` 事件会被触发。
这可被用来恢复 `input` 流。

如果 `input` 流在进程被发送到后台之前被暂停，则 `'pause'` 和 `SIGCONT` 事件不会被触发。

监听器函数被调用时不传入任何参数。

例子：

```js
rl.on('SIGTSTP', () => {
  // 这会重写 SIGTSTP，且防止程序进入后台。
  console.log('捕获 SIGTSTP。');
});
```

注意：Windows 系统不支持 `'SIGTSTP'` 事件。

