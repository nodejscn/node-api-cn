<!-- YAML
added: v0.1.98
-->

每当 `input` 流接收到接收行结束符（`\n`、`\r` 或 `\r\n`）时触发 `'line'` 事件。
通常发生在用户按下 `<Enter>` 键或 `<Return>` 键。

监听器函数被调用时会带上一个包含接收的那一行输入的字符串。

例子：

```js
rl.on('line', (input) => {
  console.log(`接收到：${input}`);
});
```

