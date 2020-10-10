<!-- YAML
added: v0.7.5
-->

每当 `input` 流恢复时，就会触发 `'resume'` 事件。

调用监听器函数时不传入任何参数。

```js
rl.on('resume', () => {
  console.log('Readline 恢复');
});
```

