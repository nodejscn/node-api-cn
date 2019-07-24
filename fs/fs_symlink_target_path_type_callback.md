<!-- YAML
added: v0.1.31
changes:
  - version: v7.6.0
    pr-url: https://github.com/nodejs/node/pull/10739
    description: The `target` and `path` parameters can be WHATWG `URL` objects
                 using `file:` protocol. Support is currently still
                 *experimental*.
  - version: v12.0.0
    pr-url: https://github.com/nodejs/node/pull/23724
    description: If the `type` argument is left undefined, Node will autodetect
                 `target` type and automatically select `dir` or `file`
-->

* `target` {string|Buffer|URL}
* `path` {string|Buffer|URL}
* `type` {string}
* `callback` {Function}
  * `err` {Error}

异步的 symlink(2)。
除了可能的异常，完成回调没有其他参数。
`type` 参数仅在 Windows 上可用，在其他平台上会被忽略。 
它可以被设置为 `'dir'`、`'file'` 或 `'junction'`。
如果未设置 `type` 参数，则 Node 将会自动检测 `target` 的类型并使用 `'file'` 或 `'dir'`。
如果 `target` 不存在，则将会使用 `'file'`。
Windows 上使用 `'junction'` 要求目标路径是绝对路径。
当使用 `'junction'` 时，`target` 参数将自动标准化为绝对路径。

示例：

```js
fs.symlink('./foo', './new-port', callback);
```

它创建了一个名为 "new-port" 且指向 "foo" 的符号链接。

