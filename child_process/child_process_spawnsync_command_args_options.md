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

* `command` {string} 要运行的命令。
* `args` {string[]} 字符串参数的列表。
* `options` {Object}
  * `cwd` {string} 子进程的当前工作目录。
  * `input` {string|Buffer|TypedArray|DataView} 该值将会作为 stdin 传给衍生的进程。提供此值将会覆盖 `stdio[0]`。
  * `argv0` {string} 显式地设置发送给子进程的 `argv[0]` 的值。如果没有指定，则将会被设置为 `command` 的值。
  * `stdio` {string|Array} 子进程的 stdio 配置。
  * `env` {Object} 环境变量的键值对。**默认值:** `process.env`。
  * `uid` {number} 设置进程的用户标识，参阅 setuid(2)。
  * `gid` {number} 设置进程的群组标识，参阅 setgid(2)。
  * `timeout` {number} 允许进程运行的最长时间，以毫秒为单位。**默认值:** `undefined`。
  * `killSignal` {string|integer} 当衍生的进程将被终止时使用的信号值。**默认值:** `'SIGTERM'`。
  * `maxBuffer` {number} stdout 或 stderr 上允许的最大字节数。如果超过限制，则子进程会被终止并且截断任何输出。参阅 [maxBuffer 与 Unicode][`maxBuffer` and Unicode] 中的警告。**默认值:** `1024 * 1024`。
  * `encoding` {string} 用于所有 stdio 输入和输出的字符编码。**默认值:** `'buffer'`。
  * `shell` {boolean|string} 如果为 `true`，则在 shell 中运行 `command`。
     在 Unix 上使用 `'/bin/sh'`，在 Windows 上使用 `process.env.ComSpec`。
     可以将不同的 shell 指定为字符串。
     参阅 [shell 的要求][Shell Requirements]与 [Windows 默认的 shell][Default Windows Shell]。
     **默认值:** `false`（没有 shell）。
  * `windowsVerbatimArguments` {boolean} 在 Windows 上不为参数加上引号或转义。在 Unix 上忽略。如果指定了 `shell` 并且是 CMD，则自动设为 `true`。**默认值:** `false`。
  * `windowsHide` {boolean} 隐藏子进程的控制台窗口（在 Windows 系统上通常会创建）。**默认值:** `false`。
* 返回: {Object}
  * `pid` {number} 子进程的 pid。
  * `output` {Array} stdio 输出的结果数组。
  * `stdout` {Buffer|string} `output[1]` 的内容。
  * `stderr` {Buffer|string} `output[2]` 的内容。
  * `status` {number} 子进程的退出码，如果子进程因信号而终止，则为 `null`。
  * `signal` {string} 用于杀死子进程的信号，如果子进程不是因信号而终止，则为 `null`。
  * `error` {Error} 如果子进程失败或超时的错误对象。

`child_process.spawnSync()` 方法通常与 [`child_process.spawn()`] 相同，但在子进程完全关闭之前该函数不会返回。
当遇到超时并发送 `killSignal` 时，该方法也需等到进程完全退出后才返回。
如果进程拦截并处理了 `SIGTERM` 信号但未退出，则父进程将会等待直到子进程退出。

如果启用了 `shell` 选项，则不要将未经过处理的用户输入传给此函数。
包含 shell 元字符的任何输入都可用于触发任意命令的执行。



