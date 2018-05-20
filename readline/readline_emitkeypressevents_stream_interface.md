<!-- YAML
added: v0.7.7
-->

* `stream` {stream.Readable}
* `interface` {readline.Interface}

`readline.emitKeypressEvents()` 方法使给定的[可读流] `stream` 相应于接收到的输入触发 `'keypress'` 事件。

可选的 `interface` 指定了一个 `readline.Interface` 实例，用于当自动补全被禁用时检测到复制粘贴输入。

如果 `stream` 是一个 [TTY]，则它必须为原始模式。

*注意*: 如果`input`是一个终端，任何一个readline实例一点有`input`，这都会被自动调用。
关闭`readline`实例不能使`input`停止发射`'keypress'`事件。

```js
readline.emitKeypressEvents(process.stdin);
if (process.stdin.isTTY)
  process.stdin.setRawMode(true);
```

