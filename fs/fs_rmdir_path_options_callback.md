<!-- YAML
added: v0.0.2
changes:
  - version: v12.10.0
    pr-url: https://github.com/nodejs/node/pull/29168
    description: The `recursive`, `maxBusyTries`, and `emfileWait` options are
                 now supported.
  - version: v10.0.0
    pr-url: https://github.com/nodejs/node/pull/12562
    description: The `callback` parameter is no longer optional. Not passing
                 it will throw a `TypeError` at runtime.
  - version: v7.6.0
    pr-url: https://github.com/nodejs/node/pull/10739
    description: The `path` parameters can be a WHATWG `URL` object using
                 `file:` protocol. Support is currently still *experimental*.
  - version: v7.0.0
    pr-url: https://github.com/nodejs/node/pull/7897
    description: The `callback` parameter is no longer optional. Not passing
                 it will emit a deprecation warning with id DEP0013.
-->

> 稳定性: 1 - 递归的删除是实验性的。

* `path` {string|Buffer|URL}
* `options` {Object}
  * `emfileWait` {integer} 如果遇到 `EMFILE` 错误，则 Node.js 将会在每次尝试时以 1 毫秒的线性回退重试该操作，直到超时持续时间超过此限制。 
    如果 `recursive` 选项不为 `true`，则忽略此选项。**默认值:** `1000`。
  * `maxBusyTries` {integer} 如果遇到 `EBUSY`、`ENOTEMPTY` 或 `EPERM` 错误，则 Node.js 将会在每次尝试时以 100 毫秒的线性回退等待重试该操作。
    此选项代表重试的次数。如果 `recursive` 选项不为 `true`，则忽略此选项。**默认值:** `3`。
  * `recursive` {boolean} 如果为 `true`，则执行递归的目录删除。在递归模式中，如果 `path` 不存在则不报告错误，并且在失败时重试操作。**默认值:** `false`。
* `callback` {Function}
  * `err` {Error}

异步的 rmdir(2)。
除了可能的异常，完成回调没有其他参数。

在文件（而不是目录）上使用 `fs.rmdir()` 会导致在 Windows 上出现 `ENOENT` 错误、在 POSIX 上出现 `ENOTDIR` 错误。

