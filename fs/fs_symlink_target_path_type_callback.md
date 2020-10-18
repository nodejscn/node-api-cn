<!-- YAML
added: v0.1.31
changes:
  - version: v12.0.0
    pr-url: https://github.com/nodejs/node/pull/23724
    description: If the `type` argument is left undefined, Node will autodetect
                 `target` type and automatically select `dir` or `file`.
  - version: v7.6.0
    pr-url: https://github.com/nodejs/node/pull/10739
    description: The `target` and `path` parameters can be WHATWG `URL` objects
                 using `file:` protocol. Support is currently still
                 *experimental*.
-->

* `target` {string|Buffer|URL}
* `path` {string|Buffer|URL}
* `type` {string}
* `callback` {Function}
  * `err` {Error}

异步的 symlink(2)，它会创建名为 `path` 的链接，该链接指向 `target`。
除了可能的异常，完成回调没有其他参数。

`type` 参数仅在 Windows 上可用，在其他平台上则会被忽略。 
它可以被设置为 `'dir'`、`'file'` 或 `'junction'`。
如果未设置 `type` 参数，则 Node.js 将会自动检测 `target` 的类型并使用 `'file'` 或 `'dir'`。
如果 `target` 不存在，则将会使用 `'file'`。
Windows 上的连接点要求目标路径是绝对路径。
当使用 `'junction'` 时，`target` 参数将会自动地标准化为绝对路径。

相对目标是相对于链接的父目录。

```js
fs.symlink('./mew', './example/mewtwo', callback);
```

上面的示例中，在 `example` 中创建了符号链接 `mewtwo`，它指向同一目录中的 `mew`：

```bash
$ tree example/
example/
├── mew
└── mewtwo -> ./mew
```

