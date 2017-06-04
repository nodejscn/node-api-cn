<!-- YAML
added: v0.4.2
changes:
  - version: v7.6.0
    pr-url: https://github.com/nodejs/node/pull/10739
    description: The `path` parameter can be a WHATWG `URL` object using `file:`
                 protocol. Support is currently still *experimental*.
  - version: v7.0.0
    pr-url: https://github.com/nodejs/node/pull/7897
    description: The `callback` parameter is no longer optional. Not passing
                 it will emit a deprecation warning.
  - version: v4.1.0
    pr-url: https://github.com/nodejs/node/pull/2387
    description: Numeric strings, `NaN` and `Infinity` are now allowed
                 time specifiers.
-->

* `path` {string|Buffer|URL}
* `atime` {integer}
* `mtime` {integer}
* `callback` {Function}

改变指定的路径所指向的文件的文件时间戳。

注意：`atime` 和 `mtime` 参数遵循以下规则：

- 值应该是一个以秒为单位的 Unix 时间戳。
  例如，`Date.now()` 返回毫秒，所以在传入前应该除以1000。
- 如果值是一个数值字符串，如 `'123456789'`，则该值会被转换为对应的数值。
- 如果值是 `NaN` 、 `Infinity` 或 `-Infinity`，则会抛出错误。

