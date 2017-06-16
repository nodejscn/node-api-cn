<!-- YAML
added: v0.7.7
-->

* `stream` {Readable}
* `interface` {readline.Interface}

`readline.emitKeypressEvents()` 方法使给定的[可写流] `stream` 相应于接收到的输入触发 `'keypress'` 事件。

可选的 `interface` 指定了一个 `readline.Interface` 实例，用于当自动补全被禁用时检测到复制粘贴输入。

如果 `stream` 是一个 [TTY]，则它必须为原始模式。

*Note*: This is automatically called by any readline instance on its `input`
if the `input` is a terminal. Closing the `readline` instance does not stop
the `input` from emitting `'keypress'` events.

```js
readline.emitKeypressEvents(process.stdin);
if (process.stdin.isTTY)
  process.stdin.setRawMode(true);
```

