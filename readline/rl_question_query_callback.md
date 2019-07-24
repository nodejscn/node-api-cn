<!-- YAML
added: v0.3.3
-->

* `query` {string} 要写入 `output` 的语句或询问，前置于提示符。
* `callback` {Function} 回调函数，调用时传入用户的输入以响应 `query`。

`rl.question()` 方法通过将 `query` 写入 `output` 来显示它，并等待用户在 `input` 上提供输入，然后调用 `callback` 函数将提供的输入作为第一个参数传入。

当调用时，如果 `input` 流已暂停，则 `rl.question()` 将恢复 `input` 流。

如果 `readline.Interface` 创建时 `output` 被设置为 `null` 或 `undefined`，则不会写入 `query`。

用法示例：

```js
rl.question('你最喜欢的食物是什么？', (answer) => {
  console.log(`你最喜欢的食物是 ${answer}`);
});
```

传给 `rl.question()` 的 `callback` 函数不遵循接受 `Error` 对象或 `null` 作为第一个参数的经典模式。
调用 `callback` 时使用提供的答案作为唯一的参数。


