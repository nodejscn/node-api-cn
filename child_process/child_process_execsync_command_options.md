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
-->

* `command` {string} 要运行的命令。
* `options` {Object}
  * `cwd` {string} 子进程的当前工作目录。
  * `input` {string|Buffer|TypedArray|DataView} 该值将会作为 stdin 传给衍生的进程。提供此值将会覆盖 `stdio[0]`。
  * `stdio` {string|Array} 子进程的 stdio 配置。默认情况下，除非指定了 `stdio`，否则 `stderr` 将会被输出到父进程的 stderr。**默认值:** `'pipe'`。
  * `env` {Object} 环境变量的键值对。**默认值:** `process.env`。
  * `shell` {string} 用于执行命令的 shell。参阅 [shell 的要求][Shell Requirements]与 [Windows 默认的 shell][Default Windows Shell]。
     **默认值:** Unix 上是 `'/bin/sh'`，Windows 上是 `process.env.ComSpec`。
  * `uid` {number} 设置进程的用户标识，参阅 setuid(2)。
  * `gid` {number} 设置进程的群组标识，参阅 setgid(2)。
  * `timeout` {number} 允许进程运行的最长时间，以毫秒为单位。**默认值:** `undefined`。
  * `killSignal` {string|integer} 当衍生的进程将被终止时使用的信号值。**默认值:** `'SIGTERM'`。
  * `maxBuffer` {number} stdout 或 stderr 上允许的最大字节数。如果超过限制，则子进程会被终止并且截断任何输出。参阅 [maxBuffer 与 Unicode][`maxBuffer` and Unicode] 中的警告。**默认值:** `1024 * 1024`。
  * `encoding` {string} 用于所有 stdio 输入和输出的字符编码。**默认值:** `'buffer'`。
  * `windowsHide` {boolean} 隐藏子进程的控制台窗口（在 Windows 系统上通常会创建）。**默认值:** `false`。
* 返回: {Buffer|string} 命令的 stdout。

`child_process.execSync()` 方法通常与 [`child_process.exec()`] 相同，但该方法在子进程完全关闭之前不会返回。
当遇到超时并发送 `killSignal` 时，该方法也需等到进程完全退出后才返回。
如果子进程拦截并处理了 `SIGTERM` 信号但未退出，则父进程将会等待直到子进程退出。

如果进程超时或具有非零的退出码，则此方法将会抛出错误。 
[`Error`] 对象将会包含 [`child_process.spawnSync()`] 的完整结果。

切勿将未经过处理的用户输入传给此函数。
包含 shell 元字符的任何输入都可用于触发任意命令的执行。

