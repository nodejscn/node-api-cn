<!-- YAML
added: v0.11.12
changes:
  - version: v8.0.0
    pr-url: https://github.com/nodejs/node/pull/10653
    description: The `input` option can now be a `Uint8Array`.
-->

* `command` {string} 要运行的命令
* `options` {Object}
  * `cwd` {string} 子进程的当前工作目录
  * `input` {string|Buffer|Uint8Array}} 要作为 stdin 传给衍生进程的值
    - 提供该值会覆盖 `stdio[0]`
  * `stdio` {string|Array} 子进程的 stdio 配置。（默认: `'pipe'`）
    - `stderr` 默认会输出到父进程中的 stderr，除非指定了 `stdio`
  * `env` {Object} 环境变量键值对
  * `shell` {string} 用于执行命令的 shell
    （默认：在 UNIX 上为 `'/bin/sh'`，在 Windows 上为 `process.env.ComSpec`。
    See [Shell Requirements][] and [Default Windows Shell][].）
  * `uid` {number} 设置该进程的用户标识。（详见 setuid(2)）
  * `gid` {number} 设置该进程的组标识。（详见 setgid(2)）
  * `timeout` {number} 进程允许运行的最大时间数，以毫秒为单位。（默认: `undefined`）
  * `killSignal` {string|integer} 当衍生进程将被杀死时要使用的信号值。（默认: `'SIGTERM'`）
  * [`maxBuffer`][] {number} stdout 或 stderr 允许的最大字节数。
    默认为 `200*1024`。
    如果超过限制，则子进程会被终止。
    See caveat at [`maxBuffer` and Unicode][].
  * `encoding` {string} 用于所有 stdio 输入和输出的编码。（默认: `'buffer'`）
* 返回: {Buffer|string} 该命令的 stdout

`child_process.execSync()` 方法与 [`child_process.exec()`] 基本相同，除了该方法直到子进程完全关闭后才返回。
当遇到超时且发送了 `killSignal` 时，则该方法直到进程完全退出后才返回结果。
注意，如果子进程拦截并处理了 `SIGTERM` 信号且没有退出，则父进程会一直等待直到子进程退出。

如果进程超时，或有一个非零的退出码，则该方法会抛出错误。
[`Error`] 对象会包含从 [`child_process.spawnSync()`] 返回的整个结果。

注意：不要把未经检查的用户输入传入到该函数。
任何包括 shell 元字符的输入都可被用于触发任何命令的执行。

