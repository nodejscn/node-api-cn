<!-- YAML
added: v0.3.3
-->

* `query` {string} 一个在提示符之前、要写入 `output` 的叙述或询问。
* `callback` {Function} 一个回调函数，它会被调用并带上用户响应 `query` 的输入。

`rl.question()` 方法通过写入到 `output` 来展示 `query`，并等待用户提供到 `input` 的输入，然后调用 `callback` 函数并传入提供的输入作为第一个参数。

当被调用时，如果 `input` 流已被暂停，则 `rl.question()` 会恢复 `input` 流。

如果 `readline.Interface` 被创建时 `output` 被设为 `null` 或 `undefined`，则 `query` 不会被写入。

例子：

```js
rl.question('你最喜欢的食物是什么？ ', (answer) => {
  console.log(`你最喜欢的食物是 ${answer}`);
});
```

注意：传入的 `rl.question()` 的 `callback` 函数不遵循接受一个 `Error` 对象或 `null` 作为第一个参数的标准模式。
`callback` 被调用时只带上提供的答案作为唯一的参数。

