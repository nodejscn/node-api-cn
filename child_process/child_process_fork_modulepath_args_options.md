<!-- YAML
added: v0.5.0
changes:
  - version: v8.0.0
    pr-url: https://github.com/nodejs/node/pull/10866
    description: The `stdio` option can now be a string.
  - version: v6.4.0
    pr-url: https://github.com/nodejs/node/pull/7811
    description: The `stdio` option is supported now.
-->

* `modulePath` {string} 在子进程运行的模块。
* `args` {string[]} 参数列表。
* `options` {Object}
  * `cwd` {string} 子进程的当前工作目录。
  * `env` {Object} 环境变量键值对。
  * `execPath` {string} 用于创建子进程的可执行文件。
  * `execArgv` {string[]} 传给可执行文件的参数列表。默认为 `process.execArgv`。
  * `silent` {boolean} 如果设为 `true`，则子进程的 stdin、 stdout 和 stderr 会传给父进程，否则从父进程继承，详见 [`child_process.spawn()`] 的 [`stdio`] 中的 `'pipe'` 和 `'inherit'`。默认为 `false`。
  * `stdio` {Array|string} 详见 `child_process.spawn()` 的 [`stdio`]。如果指定了该选项，则覆盖 `silent` 选项。
    如果使用数组，则必须包含一个值为 `'ipc'` 的元素，否则会抛出错误。例如 `[0, 1, 2, 'ipc']`。
  * `windowsVerbatimArguments` {boolean} 在 Windows 上是否为参数加引号或转义。默认为 `false`。
  * `uid` {number} 进程的用户标识，参阅 setuid(2)。
  * `gid` {number} 进程的群组标识，参阅 setgid(2)。
* 返回: {ChildProcess}

`child_process.fork()` 是 [`child_process.spawn()`] 的一个特殊情况，用于专门衍生新的 Node.js 进程。
返回的 `ChildProcess` 有一个额外的内置通信通道，允许消息在父进程和子进程之间来回传递。
详见 [`subprocess.send()`]。

衍生的 Node.js 子进程与两者之间建立的 IPC 通信信道的异常是独立于父进程的。
每个进程都有自己的内存，使用自己的 V8 实例。
由于需要额外的资源分配，因此不建议衍生大量的 Node.js 进程。

默认情况下，`child_process.fork()` 会使用父进程中的 [`process.execPath`] 衍生新的 Node.js 实例。
`options` 的 `execPath` 可以指定要使用的可执行文件。

使用自定义的 `execPath` 启动的 Node.js 进程，会使用子进程的环境变量 `NODE_CHANNEL_FD` 中指定的文件描述符与父进程通信。

不像 POSIX 的 fork(2)，`child_process.fork()` 不会克隆当前进程。

