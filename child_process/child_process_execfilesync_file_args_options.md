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
  - version: v6.2.1, v4.5.0
    pr-url: https://github.com/nodejs/node/pull/6939
    description: The `encoding` option can now explicitly be set to `buffer`.
-->

* `file` {string} 要运行的可执行文件的名称或路径。
* `args` {string[]} 字符串参数的列表。
* `options` {Object}
  * `cwd` {string} 子进程的当前工作目录。
  * `input` {string|Buffer|TypedArray|DataView} 该值会作为 stdin 传给衍生的进程。提供此值会覆盖 `stdio[0]`。
  * `stdio` {string|Array} 子进程的 stdio 配置。除非指定了 `stdio`，否则 `stderr` 默认会被输出到父进程的 stderr。**默认值:** `'pipe'`。
  * `env` {Object} 环境变量的键值对。**默认值:** `process.env`。
  * `uid` {number} 设置进程的用户标识，参见 setuid(2)。
  * `gid` {number} 设置进程的群组标识，参见 setgid(2)。
  * `timeout` {number} 允许进程运行的最长时间，以毫秒为单位。**默认值:** `undefined`。
  * `killSignal` {string|integer} 当衍生的进程被杀死时使用的信号值。**默认值:** `'SIGTERM'`。
  * `maxBuffer` {number} stdout 或 stderr 上允许的最大数据量（以字节为单位）。
    如果超过限制，则子进程会被终止。
    参见 [maxBuffer 和 Unicode][`maxBuffer` and Unicode] 的注意事项。
    **默认值:** `1024 * 1024`。
  * `encoding` {string} 用于所有 stdio 输入和输出的字符编码。**默认值:** `'buffer'`。
  * `windowsHide` {boolean} 隐藏子进程的控制台窗口（在 Windows 系统上通常会创建）。**默认值:** `false`。
  * `shell` {boolean|string} 如果为 `true`，则在 shell 中运行 `command`。
     在 Unix 上使用 `'/bin/sh'`，在 Windows 上使用 `process.env.ComSpec`。
     可以将不同的 shell 指定为字符串。
     参见 [shell 的要求][Shell requirements]和[默认的 Windows shell][Default Windows shell]。
     **默认值:** `false`（没有 shell）。
* 返回: {Buffer|string} 命令的 stdout。

`child_process.execFileSync()` 方法通常与 [`child_process.execFile()`] 相同，但该方法在子进程完全关闭之前不会返回。
当遇到超时并且已发送 `killSignal` 时，该方法也需等到进程完全退出后才返回。

如果子进程拦截并处理了 `SIGTERM` 信号但未退出，则父进程仍将等待子进程退出。

如果进程超时或具有非零的退出码，则此方法将抛出一个 [`Error`]，其中包含底层 [`child_process.spawnSync()`] 的完整结果。

**如果启用了 `shell` 选项，则不要将未经过处理的用户输入传给此函数。
包含 shell 元字符的任何输入都可用于触发任意命令的执行。**


