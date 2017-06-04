<!-- YAML
added: v0.7.5
-->

当一个 Node.js 进程使用 `<ctrl>-Z`（也就是 `SIGTSTP`）移入后台之后再使用 fg(1p) 移回前台时，触发 `'SIGCONT'` 事件。

如果 `input` 流在 `SIGTSTP` 请求之前被暂停，则事件不会被触发。

监听器函数被调用时不传入任何参数。

例子：

```js
rl.on('SIGCONT', () => {
  // `prompt` 会自动恢复流
  rl.prompt();
});
```

注意：Windows 系统不支持 `'SIGCONT'` 事件。

