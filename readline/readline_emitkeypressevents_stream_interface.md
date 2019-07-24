<!-- YAML
added: v0.7.7
-->

* `stream` {stream.Readable}
* `interface` {readline.Interface}

`readline.emitKeypressEvents()` 方法使给定的[可读流][Readable]开始触发与接收的输入相对应的 `'keypress'` 事件。

可选的 `interface` 指定 `readline.Interface` 实例，当检测到复制粘贴输入时，将禁用自动补全。

如果 `stream` 是 [TTY]，则它必须处于原始模式。

如果 `input` 是终端，则由其 `input` 上的任何 `readline` 实例自动调用。
关闭 `readline` 实例不会阻止 `input` 触发 `'keypress'` 事件。

```js
readline.emitKeypressEvents(process.stdin);
if (process.stdin.isTTY)
  process.stdin.setRawMode(true);
```

