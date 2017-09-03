<!-- YAML
added: v0.11.12
changes:
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

* `command` {string} 要运行的命令
* `args` {Array} 字符串参数列表
* `options` {Object}
  * `cwd` {string} 子进程的当前工作目录
  * `input` {string|Buffer|Uint8Array} 要作为 stdin 传给衍生进程的值
    - 提供该值会覆盖 `stdio[0]`
  * `stdio` {string|Array} 子进程的 stdio 配置
  * `env` {Object} 环境变量键值对
  * `uid` {number} 设置该进程的用户标识。（详见 setuid(2)）
  * `gid` {number} 设置该进程的组标识。（详见 setgid(2)）
  * `timeout` {number} 进程允许运行的最大时间数，以毫秒为单位。（默认: `undefined`）
  * `killSignal` {string|integer} 当衍生进程将被杀死时要使用的信号值。（默认: `'SIGTERM'`）
  * [`maxBuffer`][] {number} stdout 或 stderr 允许的最大字节数。
    默认为 `200*1024`。
    如果超过限制，则子进程会被终止。
    See caveat at [`maxBuffer` and Unicode][].
  * `encoding` {string} 用于所有 stdio 输入和输出的编码。（默认: `'buffer'`）
  * `shell` {boolean|string} 如果为 `true`，则在一个 shell 中运行 `command`。
    在 UNIX 上使用 `'/bin/sh'`，在 Windows 上使用 `process.env.ComSpec`。
    一个不同的 shell 可以被指定为字符串。
    See [Shell Requirements][] and [Default Windows Shell][].
    默认为 `false`（没有 shell）。
* 返回: {Object}
  * `pid` {number} 子进程的 pid
  * `output` {Array} stdio 输出返回的结果数组
  * `stdout` {Buffer|string} `output[1]` 的内容 
  * `stderr` {Buffer|string} `output[2]` 的内容
  * `status` {number} 子进程的退出码
  * `signal` {string} 用于杀死子进程的信号
  * `error` {Error} 如果子进程失败或超时产生的错误对象

`child_process.spawnSync()` 方法与 [`child_process.spawn()`] 基本相同，除了该方法直到子进程完全关闭后才返回。
当遇到超时且发送了 `killSignal` 时，则该方法直到进程完全退出后才返回结果。
注意，如果子进程拦截并处理了 `SIGTERM` 信号且没有退出，则父进程会一直等待直到子进程退出。

注意：不要把未经检查的用户输入传入到该函数。
任何包括 shell 元字符的输入都可被用于触发任何命令的执行。

