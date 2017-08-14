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

* `modulePath` {string} 要在子进程中运行的模块
* `args` {Array} 字符串参数列表
* `options` {Object}
  * `cwd` {string} 子进程的当前工作目录
  * `env` {Object} 环境变量键值对
  * `execPath` {string} 用来创建子进程的执行路径
  * `execArgv` {Array} 要传给执行路径的字符串参数列表
    （默认: `process.execArgv`）
  * `silent` {boolean} 如果为 `true`，则子进程中的 stdin、 stdout 和 stderr 会被导流到父进程中，否则它们会继承自父进程，详见 [`child_process.spawn()`] 的 [`stdio`] 中的 `'pipe'` 和 `'inherit'` 选项。
    （默认: `false`）
  * `stdio` {Array|string} 详见 [`child_process.spawn()`] 的 [`stdio`]。
    当提供了该选项，则它会覆盖 `silent`。
    如果使用了数组变量，则该数组必须包含一个值为 `'ipc'` 的子项，否则会抛出错误。
    例如 `[0, 1, 2, 'ipc']`。
  * `uid` {number} 设置该进程的用户标识。（详见 setuid(2)）
  * `gid` {number} 设置该进程的组标识。（详见 setgid(2)）
* 返回: {ChildProcess}

`child_process.fork()` 方法是 [`child_process.spawn()`] 的一个特殊情况，专门用于衍生新的 Node.js 进程。
跟 [`child_process.spawn()`] 一样返回一个 [`ChildProcess`] 对象。
返回的 [`ChildProcess`] 会有一个额外的内置的通信通道，它允许消息在父进程和子进程之间来回传递。
详见 [`subprocess.send()`]。

衍生的 Node.js 子进程与两者之间建立的 IPC 通信信道的异常是独立于父进程的。
每个进程都有自己的内存，使用自己的 V8 实例。
由于需要额外的资源分配，因此不推荐衍生大量的 Node.js 进程。

默认情况下，`child_process.fork()` 会使用父进程中的 [`process.execPath`] 衍生新的 Node.js 实例。
`options` 对象中的 `execPath` 属性可以替换要使用的执行路径。

使用自定义的 `execPath` 启动的 Node.js 进程，会使用子进程的环境变量 `NODE_CHANNEL_FD` 中指定的文件描述符（fd）与父进程通信。
fd 上的输入和输出期望被分割成一行一行的 JSON 对象。

注意，不像 POSIX 系统回调中的 fork(2)，`child_process.fork()` 不会克隆当前进程。

