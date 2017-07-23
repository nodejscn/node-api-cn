<!-- YAML
added: v0.7.1
changes:
  - version: 8.2.0
    pr-url: https://github.com/nodejs/node/pull/14140
    description: The `inspectPort` option is supported now.
  - version: v6.4.0
    pr-url: https://github.com/nodejs/node/pull/7838
    description: The `stdio` option is supported now.
-->

* {Object}
  * `execArgv` {Array} 传递给Node.js可执行文件的参数列表。 (Default=`process.execArgv`)
  * `exec` {string} worker文件路径。 (Default=`process.argv[1]`)
  * `args` {Array} 传递给worker的参数。(Default=`process.argv.slice(2)`)
  * `silent` {boolean} 是否需要发送输出值父进程的stdio。(Default=`false`)
  * `stdio` {Array} 配置fork进程的stdio。  由于cluster模块运行依赖于IPC，这个配置必须包含`'ipc'`。当提供了这个选项后，将撤销`silent`。
  * `uid` {number} 设置进程的user标识符。 (见 setuid(2).)
  * `gid` {number} 设置进程的group标识符。 (见 setgid(2).)
  * `inspectPort` {number|function} Sets inspector port of worker.
    This can be a number, or a function that takes no arguments and returns a
    number. By default each worker gets its own port, incremented from the
    master's `process.debugPort`.

调用`.setupMaster()` (或 `.fork()`)后，这个settings对象将会包含这些设置项，包括默认值。

这个对象不打算被修改或手动设置。
