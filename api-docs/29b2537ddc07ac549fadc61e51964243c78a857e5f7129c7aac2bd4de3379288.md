<!-- YAML
added: v0.1.98
-->

* `data` {string}
* `key` {Object}
  * `ctrl` {boolean} `true` 表示 `<ctrl>` 键。
  * `meta` {boolean} `true` 表示 `<Meta>` 键。
  * `shift` {boolean} `true` 表示 `<Shift>` 键。
  * `name` {string} 按键的名称。

`rl.write()` 方法将 `data` 或 `key` 标识的按键序列写入 `output`。
仅当 `output` 是 [TTY] 文本终端时才支持 `key` 参数。

如果指定了 `key`，则忽略 `data`。

当调用时，如果 `input` 流已暂停，则 `rl.write()` 将恢复它。

如果 `readline.Interface` 创建时 `output` 被设置为 `null` 或 `undefined`，则不会写入 `data` 和 `key`。

```js
rl.write('删除这个！');
// 模拟 Ctrl+u 删除先前写入的行。
rl.write(null, { ctrl: true, name: 'u' });
```

`rl.write()` 方法将数据写入 `readline` 的 `Interface` 的 `input`，就像它是由用户提供的一样。

