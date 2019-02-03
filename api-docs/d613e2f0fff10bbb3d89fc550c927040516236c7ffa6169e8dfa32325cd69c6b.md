<!-- YAML
added: v0.7.5
-->

当先前使用 `<ctrl>-Z`（即 `SIGTSTP`）移入后台的 Node.js 进程使用 fg(1p) 返回到前台时，就会触发 `'SIGCONT'` 事件。

如果 `input` 流在 `SIGTSTP` 请求之前被暂停，则不会触发此事件。

调用监听器函数时不传入任何参数。

```js
rl.on('SIGCONT', () => {
  // `prompt` 将自动恢复流。
  rl.prompt();
});
```

Windows 上不支持 `'SIGCONT'` 事件。

