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

*请注意*: 在文件上（而不是目录上）使用`fs.rmdirSync()`，在Windows平台将会导致`ENOENT`错误，而在POSIX平台将会导致`ENOTDIR`错误。

