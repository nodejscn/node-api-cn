<!-- YAML
added: v0.1.21
changes:
  - version: v7.6.0
    pr-url: https://github.com/nodejs/node/pull/10739
    description: The `path` parameters can be a WHATWG `URL` object using
                 `file:` protocol. Support is currently still *experimental*.
-->

* `path` {string|Buffer|URL}

同步的 rmdir(2)。返回 `undefined`。

在文件（而不是目录）上使用 `fs.rmdirSync()` 会导致在 Windows 上出现 `ENOENT` 错误、在 POSIX 上出现 `ENOTDIR` 错误。

