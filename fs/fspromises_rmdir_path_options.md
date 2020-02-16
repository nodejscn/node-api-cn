<!-- YAML
added: v10.0.0
changes:
  - version: v12.16.0
    pr-url: https://github.com/nodejs/node/pull/30644
    description: The `maxBusyTries` option is renamed to `maxRetries`, and its
                 default is 0. The `emfileWait` option has been removed, and
                 `EMFILE` errors use the same retry logic as other errors. The
                 `retryDelay` option is now supported. `ENFILE` errors are now
                 retried.
  - version: v12.10.0
    pr-url: https://github.com/nodejs/node/pull/29168
    description: The `recursive`, `maxBusyTries`, and `emfileWait` options are
                  now supported.
-->

> 稳定性: 1 - 递归的删除是实验性的。

* `path` {string|Buffer|URL}
* `options` {Object}
  * `maxRetries` {integer} 如果遇到 `EBUSY`、`EMFILE`、`ENFILE`、`ENOTEMPTY` 或 `EPERM` 错误，则 Node.js 将会在每次尝试时以 `retryDelay` 毫秒的线性回退来重试该操作。
    此选项表示重试的次数。如果 `recursive` 选项不为 `true`，则忽略此选项。**默认值:** `0`。
  * `recursive` {boolean} 如果为 `true`，则执行递归的目录删除。在递归模式中，如果 `path` 不存在则不报告错误，并且在失败时重试操作。**默认值:** `false`。
  * `retryDelay` {integer} 重试之间等待的时间（以毫秒为单位）。如果 `recursive` 选项不为 `true`，则忽略此选项。**默认值:** `100`。
* 返回: {Promise}

删除 `path` 指定的目录，然后在成功时解决 `Promise` 且不带参数。

在文件（而不是目录）上使用 `fsPromises.rmdir()` 会导致 `Promise` 被拒绝，在 Windows 上会带上 `ENOENT` 错误、在 POSIX 上会带上 `ENOTDIR` 错误。

