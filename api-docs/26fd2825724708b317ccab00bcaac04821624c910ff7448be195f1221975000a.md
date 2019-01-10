<!-- YAML
added: v0.7.5
-->

当以下之一发生时触发 `'pause'` 事件：

* `input` 流被暂停。
* `input` 流不是暂停的，且接收到 `SIGCONT` 事件。（详见 [`SIGTSTP`] 事件和 [`SIGCONT`] 事件）

监听器函数被调用时不传入任何参数。

例子：

```js
rl.on('pause', () => {
  console.log('Readline 被暂停。');
});
```

