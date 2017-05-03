<!-- YAML
added: v0.1.31
-->

* `target` {String | Buffer}
* `path` {String | Buffer}
* `type` {String}
* `callback` {Function}

异步的 symlink(2)。
完成回调只有一个可能的异常参数。
`type` 参数可以设为 `'dir'`、`'file'` 或 `'junction'`（默认为 `'file'`），且仅在 Windows 上有效（在其他平台上忽略）。
注意，Windows 结点要求目标路径是绝对的。
当使用 `'junction'` 时，`target` 参数会被自动标准化为绝对路径。

例子：

```js
fs.symlink('./foo', './new-port', callback);
```

它创建了一个名为 "new-port" 且指向 "foo" 的符号链接。

