<!-- YAML
added: v0.11.12
changes:
  - version: v10.10.0
    pr-url: https://github.com/nodejs/node/pull/22409
    description: The `input` option can now be any `TypedArray` or a
                 `DataView`.
  - version: v8.8.0
    pr-url: https://github.com/nodejs/node/pull/15380
    description: The `windowsHide` option is supported now.
  - version: v8.0.0
    pr-url: https://github.com/nodejs/node/pull/10653
    description: The `input` option can now be a `Uint8Array`.
  - version: v6.2.1, v4.5.0
    pr-url: https://github.com/nodejs/node/pull/6939
    description: The `encoding` option can now explicitly be set to `buffer`.
-->

* `file` {string} 要运行的可执行文件的名称或路径。
* `args` {string[]} 参数列表。
* `options` {Object}
  * `cwd` {string} 子进程的当前工作目录。
  * `input` {string|Buffer|TypedArray|DataView} 作为 stdin 传给衍生进程的值。指定该值会覆盖 `stdio[0]`。
  * `stdio` {string|Array} 子进程的 stdio 配置。`stderr` 默认会输出到父进程的 stderr，除非指定了 `stdio`。默认为 `'pipe'`。
  * `env` {Object} 环境变量键值对。
  * `uid` {number} 进程的用户标识。参阅 setuid(2)。
  * `gid` {number} 进程的群组标识。参阅 setgid(2)。
  * `timeout` {number} 允许进程运行的最长时间，以毫秒为单位。默认为 `undefined`。
  * `killSignal` {string|integer} 用于杀死衍生进程的信号。默认为 `'SIGTERM'`。
  * `maxBuffer` {number} stdout 或 stderr 允许的最大字节数。如果超过限制，则子进程会终止。参阅 [`maxBuffer`与Unicode][`maxBuffer` and Unicode]。默认为 `200*1024`。
  * `encoding` {string} 用于 stdio 输入和输出的字符编码。默认为 `'buffer'`。
  * `windowsHide` {boolean} 是否隐藏子进程的控制台窗口。默认为 `false`。
  * `shell` {boolean|string} 如果设为 `true`，则在 shell 中运行 `command`。
     在 UNIX 上使用 `'/bin/sh'`，在 Windows 上使用 `process.env.ComSpec`。
     传入字符串则指定其他 `shell`。
     参阅 [Shell的要求][Shell Requirements]与 [Windows默认的Shell][Default Windows Shell]。
     默认为 `false`（没有 shell）。
* 返回: {Buffer|string} 命令的 stdout。

与 [`child_process.execFile()`] 的区别是，该方法需等到子进程完全关闭后才返回。
当发生超时且已发送 `killSignal` 时，该方法也需等到进程完全退出后才返回。

如果子进程拦截并处理了 `SIGTERM` 信号且没有退出，则父进程会一直等待直到子进程退出。

如果进程超时或有非零的退出码，则该方法会抛出一个 [`Error`]，这个错误对象包含了底层 [`child_process.spawnSync()`] 的完整结果。

