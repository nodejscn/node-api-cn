<!-- YAML
added: v0.4.2
changes:
  - version: v8.0.0
    pr-url: https://github.com/nodejs/node/pull/11919
    description: "`NaN`, `Infinity`, and `-Infinity` are no longer valid time
                 specifiers."
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
* `atime` {number|string|Date}
* `mtime` {number|string|Date}
* `callback` {Function}
  * `err` {Error}

改变 `path` 所指向的对象的文件系统时间戳。

`atime` 参数和 `mtime` 参数遵循以下规则：
- 值可以是 Unix 时间戳数值、`Date` 对象、或数值字符串如 `'123456789.0'`。
- 如果值不能被转换为数值，或值是 `NaN` 、 `Infinity` 或 `-Infinity`，则会抛出错误。

