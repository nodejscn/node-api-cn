<!-- YAML
added: v0.1.21
changes:
  - version: v7.6.0
    pr-url: https://github.com/nodejs/node/pull/10739
    description: The `path` parameters can be a WHATWG `URL` object using
                 `file:` protocol. Support is currently still *experimental*.
-->

* `path` {string|Buffer|URL}

移除目录。同步的 rmdir(2)。返回 `undefined`。

如果对文件（而不是对目录）使用 `fs.rmdirSync()`，则在 Windows 上会抛出 `ENOENT`，在 POSIX 上会抛出 `ENOTDIR`。

