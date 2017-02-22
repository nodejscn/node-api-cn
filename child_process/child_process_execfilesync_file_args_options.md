<!-- YAML
added: v0.11.12
-->

* `file` {String} 要运行的可执行文件的名称或路径
* `args` {Array} 字符串参数列表
* `options` {Object}
  * `cwd` {String} 子进程的当前工作目录
  * `input` {String|Buffer} 要作为 stdin 传给衍生进程的值
    - 提供该值会覆盖 `stdio[0]`
  * `stdio` {String | Array} 子进程的 stdio 配置。（默认: `'pipe'`）
    - `stderr` 默认会输出到父进程中的 stderr，除非指定了 `stdio`
  * `env` {Object} 环境变量键值对
  * `uid` {Number} 设置该进程的用户标识。（详见 setuid(2)）
  * `gid` {Number} 设置该进程的组标识。（详见 setgid(2)）
  * `timeout` {Number} 进程允许运行的最大时间数，以毫秒为单位。（默认: `undefined`）
  * `killSignal` {String|Integer} 当衍生进程将被杀死时要使用的信号值。（默认: `'SIGTERM'`）
  * [`maxBuffer`] {Number} stdout 或 stderr 允许的最大数据量（以字节为单位）。
    如果超过限制，则子进程会被终止
  * `encoding` {String} 用于所有 stdio 输入和输出的编码。（默认: `'buffer'`）
* 返回: {Buffer|String} 该命令的 stdout

`child_process.execFileSync()` 方法与 [`child_process.execFile()`] 基本相同，除了该方法直到子进程完全关闭后才返回。
当遇到超时且发送了 `killSignal` 时，则该方法直到进程完全退出后才返回结果。
注意，如果子进程拦截并处理了 `SIGTERM` 信号且没有退出，则父进程会一直等待直到子进程退出。

如果进程超时，或有一个非零的退出码，则该方法会抛出错误。
[`Error`] 对象会包含从 [`child_process.spawnSync()`] 返回的整个结果。

