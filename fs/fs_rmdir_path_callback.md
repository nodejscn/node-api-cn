<!-- YAML
added: v0.0.2
changes:
  - version: v7.6.0
    pr-url: https://github.com/nodejs/node/pull/10739
    description: The `path` parameters can be a WHATWG `URL` object using
                 `file:` protocol. Support is currently still *experimental*.
  - version: v7.0.0
    pr-url: https://github.com/nodejs/node/pull/7897
    description: The `callback` parameter is no longer optional. Not passing
                 it will emit a deprecation warning.
-->

* `path` {string|Buffer|URL}
* `callback` {Function}

异步的 rmdir(2)。
完成回调只有一个可能的异常参数。

*请注意*: 在文件上（而不是目录上）使用`fs.rmdir()`，在Windows平台将会导致`ENOENT`错误，而在POSIX平台将会导致`ENOTDIR`错误。

