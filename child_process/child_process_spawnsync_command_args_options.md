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
  - version: v5.7.0
    pr-url: https://github.com/nodejs/node/pull/4598
    description: The `shell` option is supported now.
-->

* `command` {string} 运行的命令。
* `args` {string[]} 参数列表。
* `options` {Object}
  * `cwd` {string} 子进程的当前工作目录。
  * `input` {string|Buffer|TypedArray|DataView} 传入衍生进程的 stdin。指定该值会覆盖 `stdio[0]`。
  * `argv0` {string} 发送给子进程的 `argv[0]` 的值。如果没有指定，则设为 `command` 的值。
  * `stdio` {string|Array} 子进程的 stdio 配置。
  * `env` {Object} 环境变量键值对。
  * `uid` {number} 进程的用户标识。参见 setuid(2)。
  * `gid` {number} 进程的群组标识。参见 setgid(2)。
  * `timeout` {number} 允许进程运行的最长时间，以毫秒为单位。默认为 `undefined`。
  * `killSignal` {string|integer} 用于杀死衍生进程的信号。默认为 `'SIGTERM'`。
  * `maxBuffer` {number} stdout 或 stderr 允许的最大字节数。如果超过限制，则子进程会终止。参见 [maxBuffer与Unicode][`maxBuffer` and Unicode]。默认为 `200*1024`。
  * `encoding` {string} 用于 stdio 输入和输出的字符编码。默认为 `'buffer'`。
  * `shell` {boolean|string} 如果设为 `true`，则在 shell 中运行 `command`。
     在 UNIX 上使用 `'/bin/sh'`，在 Windows 上使用 `process.env.ComSpec`。
     传入字符串则指定其他 `shell`。
     参见 [Shell的要求][Shell Requirements]与 [Windows默认的Shell][Default Windows Shell]。
     默认为 `false`（没有 shell）。
  * `windowsVerbatimArguments` {boolean} 在 Windows 上是否为参数加引号或转义。如果指定了 `shell`，则自动设为 `true`。默认为 `false`。
  * `windowsHide` {boolean} 是否隐藏子进程的控制台窗口。默认为 `false`。
* 返回: {Object}
  * `pid` {number} 子进程的 pid。
  * `output` {Array} stdio 的输出。
  * `stdout` {Buffer|string} `output[1]` 的内容。
  * `stderr` {Buffer|string} `output[2]` 的内容。
  * `status` {number} 子进程的退出码。
  * `signal` {string} 用于杀死子进程的信号。
  * `error` {Error} 如果子进程失败或超时产生的错误对象。

与 [`child_process.spawn()`] 的区别是，该方法需等到子进程完全关闭后才返回。
当发生超时且已发送 `killSignal` 时，该方法也需等到进程完全退出后才返回。
如果子进程拦截并处理了 `SIGTERM` 信号且没有退出，则父进程会一直等待直到子进程退出。


