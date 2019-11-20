<!-- YAML
added: v0.7.1
changes:
  - version: v9.5.0
    pr-url: https://github.com/nodejs/node/pull/18399
    description: The `cwd` option is supported now.
  - version: v9.4.0
    pr-url: https://github.com/nodejs/node/pull/17412
    description: The `windowsHide` option is supported now.
  - version: v8.2.0
    pr-url: https://github.com/nodejs/node/pull/14140
    description: The `inspectPort` option is supported now.
  - version: v6.4.0
    pr-url: https://github.com/nodejs/node/pull/7838
    description: The `stdio` option is supported now.
-->

* {Object}
  * `execArgv` {string[]} 传给 Node.js 可执行文件的字符串参数列表。**默认值:** `process.execArgv`。
  * `exec` {string} 工作进程的文件路径。**默认值:** `process.argv[1]`。
  * `args` {string[]} 传给工作进程的字符串参数。**默认值:** `process.argv.slice(2)`。
  * `cwd` {string} 工作进程的当前工作目录。**默认值:** `undefined`（从父进程继承）。
  * `silent` {boolean} 是否需要发送输出到父进程的 stdio。**默认值:** `false`。
  * `stdio` {Array} 配置衍生的进程的 stdio。 由于 cluster 模块运行依赖于 IPC，这个配置必须包含 `'ipc'`。如果提供了这个选项，则覆盖 `silent`。
  * `uid` {number} 设置进程的用户标识符。参阅 setuid(2)。
  * `gid` {number} 设置进程的群组标识符。参阅 setgid(2)。
  * `inspectPort` {number|Function} 设置工作进程的检查端口。这可以是一个数字、或不带参数并返回数字的函数。默认情况下，每个工作进程都有自己的端口，从主进程的 `process.debugPort` 开始递增。
  * `windowsHide` {boolean} 隐藏衍生的进程的控制台窗口（通常在 Windows 系统上会创建）。**默认值:** `false`。

调用 [`.setupMaster()`]（或 [`.fork()`]）之后，这个配置对象将会包含这些配置项，包括默认值。

这个对象不打算被修改或手动设置。

