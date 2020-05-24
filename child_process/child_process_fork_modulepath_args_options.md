<!-- YAML
added: v0.5.0
changes:
  - version:
      - v13.2.0
      - v12.16.0
    pr-url: https://github.com/nodejs/node/pull/30162
    description: 支持 `serialization` 选项。
  - version: v8.0.0
    pr-url: https://github.com/nodejs/node/pull/10866
    description: 选项 `stdio` 可以是字符串。
  - version: v6.4.0
    pr-url: https://github.com/nodejs/node/pull/7811
    description: 支持 `stdio` 选项。
-->

* `modulePath` {string} 要在子进程中运行的模块。
* `args` {string[]} 字符串参数的列表。
* `options` {Object}
  * `cwd` {string} 子进程的当前工作目录。
  * `detached` {boolean} 使子进程独立于其父进程运行。
    具体行为取决于平台，参见 [`options.detached`]。
  * `env` {Object} 环境变量的键值对。
    **默认值:** `process.env`。
  * `execPath` {string} 用于创建子进程的可执行文件。
  * `execArgv` {string[]} 传给可执行文件的字符串参数的列表。
    **默认值:** `process.execArgv`。
  * `serialization` {string} 指定用于在进程之间发送消息的序列化类型。
    可能的值为 `'json'` 和 `'advanced'`。
    详见[高级序列化][Advanced Serialization]。
    **默认值:** `'json'`。
  * `silent` {boolean} 如果为 `true`，则子进程的 stdin、stdout 和 stderr 会被 pipe 到父进程，否则它们会继承自父进程，详见 [`child_process.spawn()`] 的 [`stdio`] 中的 `'pipe'` 和 `'inherit'` 选项。
    **默认值:** `false`。
  * `stdio` {Array|string} 参见 [`child_process.spawn()`] 的 [`stdio`]。
    当提供此选项时，则它会覆盖 `silent` 选项。
    如果使用数组变量，则它必须包含值为 `'ipc'` 的元素，否则会抛出错误。
    例如 `[0, 1, 2, 'ipc']`。
  * `windowsVerbatimArguments` {boolean} 在 Windows 上不为参数加上引号或转义。
    在 Unix 上会忽略。
    **默认值:** `false`。
  * `uid` {number} 设置进程的用户标识，参见 setuid(2)。
  * `gid` {number} 设置进程的群组标识，参见 setgid(2)。
* 返回: {ChildProcess}

`child_process.fork()` 方法是 [`child_process.spawn()`] 的特例，专门用于衍生新的 Node.js 进程。
与 [`child_process.spawn()`] 一样返回 [`ChildProcess`] 对象。
返回的 [`ChildProcess`] 会内置额外的通信通道，允许消息在父进程和子进程之间来回传递。
详见 [`subprocess.send()`]。

记住，衍生的 Node.js 子进程独立于父进程，但两者之间建立的 IPC 通信通道除外。
每个进程都有自己的内存，带有自己的 V8 实例。
由于需要额外的资源分配，因此不建议衍生大量的 Node.js 子进程。

默认情况下，`child_process.fork()` 会使用父进程的 [`process.execPath`] 来衍生新的 Node.js 实例。 
`options` 对象中的 `execPath` 属性可以使用其他的执行路径。

使用自定义的 `execPath` 启动的 Node.js 进程会使用文件描述符（在子进程上使用环境变量 `NODE_CHANNEL_FD` 标识）与父进程通信。

与 fork(2) 的 POSIX 系统调用不同，`child_process.fork()` 不会克隆当前的进程。

[`child_process.spawn()`] 中可用的 `shell` 选项在 `child_process.fork()` 中不支持，如果设置则会被忽略。

