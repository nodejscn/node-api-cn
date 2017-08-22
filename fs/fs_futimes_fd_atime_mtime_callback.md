<!-- YAML
added: v0.4.2
changes:
  - version: v7.0.0
    pr-url: https://github.com/nodejs/node/pull/7897
    description: The `callback` parameter is no longer optional. Not passing
                 it will emit a deprecation warning.
  - version: v4.1.0
    pr-url: https://github.com/nodejs/node/pull/2387
    description: Numeric strings, `NaN` and `Infinity` are now allowed
                 time specifiers.
-->

* `fd` {integer}
* `atime` {integer}
* `mtime` {integer}
* `callback` {Function}

改变由所提供的文件描述符所指向的文件的文件时间戳。

*请注意*: 该函数不支持AIX 7.1以下版本，在AIX 7.1以下版本会返回`UV_ENOSYS`错误。

