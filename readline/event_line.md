<!-- YAML
added: v0.1.98
-->

每当 `input` 流接收到行尾输入（`\n`、`\r` 或 `\r\n`）时就会触发 `'line'` 事件。
这种情况通常发生在当用户按下 `<Enter>` 键或 `<Return>` 键。

调用监听器函数时会带上包含接收到的那一行输入的字符串。

```js
rl.on('line', (input) => {
  console.log(`接收到：${input}`);
});
```

