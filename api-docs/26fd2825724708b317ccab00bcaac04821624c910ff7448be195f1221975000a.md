<!-- YAML
added: v0.7.5
-->

当发生以下任一情况时会触发 `'pause'` 事件：

* `input` 流被暂停。
* `input` 流未暂停，且接收到 `'SIGCONT'` 事件。（参阅 [`'SIGTSTP'`] 事件和 [`'SIGCONT'`] 事件）

调用监听器函数时不传入任何参数。

```js
rl.on('pause', () => {
  console.log('Readline 暂停');
});
```

