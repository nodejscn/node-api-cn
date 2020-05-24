<!-- YAML
added: v0.11.12
changes:
  - version: v10.10.0
    pr-url: https://github.com/nodejs/node/pull/22409
    description: 选项 `input` 可以是任何 `TypedArray` 或 `DataView`。
  - version: v8.8.0
    pr-url: https://github.com/nodejs/node/pull/15380
    description: 支持 `windowsHide` 选项。
  - version: v8.0.0
    pr-url: https://github.com/nodejs/node/pull/10653
    description: 选项 `input` 可以是 `Uint8Array`。
-->

* `command` {string} 要运行的命令。
* `options` {Object}
  * `cwd` {string} 子进程的当前工作目录。
  * `input` {string|Buffer|TypedArray|DataView} 该值会作为 stdin 传给衍生的进程。
    提供此值会覆盖 `stdio[0]`。
  * `stdio` {string|Array} 子进程的 stdio 配置。
    除非指定了 `stdio`，否则 `stderr` 默认会被输出到父进程的 stderr。
    **默认值:** `'pipe'`。
  * `env` {Object} 环境变量的键值对。
    **默认值:** `process.env`。
  * `shell` {string} 用于执行命令。
    参见 [shell 的要求][Shell Requirements]和[默认的 Windows shell][Default Windows Shell]。
    **默认值:** Unix 上是 `'/bin/sh'`，Windows 上是 `process.env.ComSpec`。
  * `uid` {number} 设置进程的用户标识，参见 setuid(2)。
  * `gid` {number} 设置进程的群组标识，参见 setgid(2)。
  * `timeout` {number} 允许进程运行的最长时间，以毫秒为单位。
    **默认值:** `undefined`。
  * `killSignal` {string|integer} 当衍生的进程被杀死时使用的信号值。
    **默认值:** `'SIGTERM'`。
  * `maxBuffer` {number} stdout 或 stderr 上允许的最大数据量（以字节为单位）。
    如果超过限制，则子进程会被终止，并且输出会被截断。
    参见 [maxBuffer 和 Unicode][`maxBuffer` and Unicode] 的注意事项。
    **默认值:** `1024 * 1024`。
  * `encoding` {string} 用于所有 stdio 输入和输出的字符编码。
    **默认值:** `'buffer'`。
  * `windowsHide` {boolean} 隐藏子进程的控制台窗口（在 Windows 系统上通常会创建）。
    **默认值:** `false`。
* 返回: {Buffer|string} 命令的 stdout。

`child_process.execSync()` 方法通常与 [`child_process.exec()`] 相同，但该方法在子进程完全关闭之前不会返回。
当遇到超时并且已发送 `killSignal` 时，该方法也需等到进程完全退出后才返回。
如果子进程拦截并处理了 `SIGTERM` 信号但未退出，则父进程会等待直到子进程退出。

如果进程超时或具有非零的退出码，则此方法会抛出错误。 
[`Error`] 对象会包含 [`child_process.spawnSync()`] 的完整结果。

**切勿将未经过处理的用户输入传给此函数。
包含 shell 元字符的任何输入都可用于触发任意命令的执行。**

