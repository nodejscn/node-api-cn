<!-- YAML
added: v10.0.0
changes:
  - version:
     - v13.3.0
     - v12.16.0
    pr-url: https://github.com/nodejs/node/pull/30644
    description: 选项 `maxBusyTries` 被重命名为 `maxRetries`，并且默认值为 0。
      `emfileWait` 选项已被删除，并且 `EMFILE` 错误使用与其他错误相同的重试逻辑。
      支持 `retryDelay` 选项。
      `ENFILE` 错误会被重试。
  - version: v12.10.0
    pr-url: https://github.com/nodejs/node/pull/29168
    description: The `recursive`, `maxBusyTries`, and `emfileWait` options are
                  now supported.
-->

> 稳定性: 1 - 递归的删除是实验性的。

* `path` {string|Buffer|URL}
* `options` {Object}
  * `maxRetries` {integer} 如果遇到 `EBUSY`、`EMFILE`、`ENFILE`、`ENOTEMPTY` 或 `EPERM` 错误，则 Node.js 会重试该操作（每次尝试时使用 `retryDelay` 毫秒时长的线性回退等待）。
    此选项表示重试的次数。
    如果 `recursive` 选项不为 `true`，则此选项会被忽略。
    **默认值:** `0`。
  * `recursive` {boolean} 如果为 `true`，则执行递归的目录删除。
    在递归模式中，错误不会被报告（如果 `path` 不存在），并且操作会被重试（当失败时）。
    **默认值:** `false`。
  * `retryDelay` {integer} 重试之间等待的时间（以毫秒为单位）。
    如果 `recursive` 选项不为 `true`，则此选项会被忽略。
    **默认值:** `100`。
* 返回: {Promise}

删除 `path` 指定的目录，然后在成功时解决 `Promise` 且不带参数。

对文件（而不是目录）使用 `fsPromises.rmdir()` 会导致 `Promise` 被拒绝，在 Windows 上会带上 `ENOENT` 错误、在 POSIX 上会带上 `ENOTDIR` 错误。

设置为 `recursive` 为 `true` 会导致行为类似于 Unix 命令 `rm -rf`：不存在的路径不会引发错误，表示文件的路径会被删除。 
`recursive` 选项的宽容行为已弃用，未来会抛出 `ENOTDIR` 和 `ENOENT`。
