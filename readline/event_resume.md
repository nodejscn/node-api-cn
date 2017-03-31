<!-- YAML
added: v0.7.5
-->

每当 `input` 流被恢复时触发 `'resume'` 事件。

监听器函数被调用时不传入任何参数。

例子：

```js
rl.on('resume', () => {
  console.log('Readline 被恢复。');
});
```

