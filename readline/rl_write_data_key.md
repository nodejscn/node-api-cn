<!-- YAML
added: v0.1.98
-->

* `data` {string}
* `key` {Object}
  * `ctrl` {boolean} 如果为 `true` 则表示 `<ctrl>` 键。
  * `meta` {boolean} 如果为 `true` 则表示 `<Meta>` 键。
  * `shift` {boolean} 如果为 `true` 则表示 `<Shift>` 键。
  * `name` {string} 一个按键的名称。

`rl.write()` 方法会把 `data` 或一个由 `key` 指定的按键序列写入到 `output`。
只有当 `output` 是一个 [TTY] 文本终端时，`key` 参数才被支持。

如果指定了 `key`，则 `data` 会被忽略。

当被调用时，如果 `input` 流已被暂停，则 `rl.write()` 会恢复 `input` 流。

如果 `readline.Interface` 被创建时 `output` 被设为 `null` 或 `undefined`，则 `data` 和 `key` 不会被写入。

例子：

```js
rl.write('删除这个！');
// 模拟 Ctrl+u 删除写入的前一行。
rl.write(null, { ctrl: true, name: 'u' });
```

注意：`rl.write()` 方法会写入数据到 `readline` 接口的 `input`，犹如它是用户提供的。

