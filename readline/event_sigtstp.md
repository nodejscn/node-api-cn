<!-- YAML
added: v0.7.5
-->

每当 `input` 流接收到 `<ctrl>-Z` 输入（通常称为 `SIGTSTP`）时，就会触发 `'SIGTSTP'` 事件。
如果当 `input` 流接收到 `SIGTSTP` 时没有注册 `'SIGTSTP'` 事件监听器，则 Node.js 进程将被发送到后台。

当使用 fg(1p) 恢复程序时，将触发 `'pause'` 和 `'SIGCONT'` 事件。
这可用于恢复 `input` 流。

如果在将进程发送到后台之前暂停 `input`，则不会触发 `'pause'` 和 `'SIGCONT'` 事件。

调用监听器函数时不传入任何参数。

```js
rl.on('SIGTSTP', () => {
  // 这将覆盖 SIGTSTP 并阻止程序进入后台。
  console.log('捕获 SIGTSTP');
});
```

Windows 上不支持 `'SIGTSTP'` 事件。

