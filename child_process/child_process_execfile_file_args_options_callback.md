<!-- YAML
added: v0.1.91
changes:
  - version: v8.8.0
    pr-url: https://github.com/nodejs/node/pull/15380
    description: The `windowsHide` option is supported now.
-->

* `file` {string} 要运行的可执行文件的名称或路径。
* `args` {string[]} 参数列表。
* `options` {Object}
  * `cwd` {string} 子进程的当前工作目录。
  * `env` {Object} 环境变量键值对。
  * `encoding` {string} 字符编码。默认为 `'utf8'`。
  * `timeout` {number} 默认为 `0`。
  * `maxBuffer` {number} stdout 或 stderr 允许的最大字节数。如果超过限制，则子进程会终止。参见 [`maxBuffer`与Unicode][`maxBuffer` and Unicode]。默认为 `200*1024`。
  * `killSignal` {string|integer} 默认为 `'SIGTERM'`。
  * `uid` {number} 进程的用户标识，参见 setuid(2)。
  * `gid` {number} 进程的群组标识，参见 setgid(2)。
  * `windowsHide` {boolean} 是否隐藏子进程的控制台窗口。默认为 `false`。
  * `windowsVerbatimArguments` {boolean} 在 Windows 上是否为参数加引号或转义。默认为 `false`。
  * `shell` {boolean|string} 如果设为 `true`，则在 shell 中运行 `command`。
     在 UNIX 上使用 `'/bin/sh'`，在 Windows 上使用 `process.env.ComSpec`。
     传入字符串则指定其他 `shell`。
     参见 [Shell的要求][Shell Requirements]与 [Windows默认的Shell][Default Windows Shell]。
     默认为 `false`（没有 shell）。
* `callback` {Function} 当进程终止时调用。
  * `error` {Error}
  * `stdout` {string|Buffer}
  * `stderr` {string|Buffer}
* 返回: {ChildProcess}

与 [`child_process.exec()`] 类似，除了默认不衍生 shell。
可执行的 `file` 会被直接衍生为一个新进程，这使得它比 `child_process.exec()` 更高效。

因为没有衍生 shell，所以不支持 I/O 重定向或文件查找等功能。

```js
const { execFile } = require('child_process');
const child = execFile('node', ['--version'], (error, stdout, stderr) => {
  if (error) {
    throw error;
  }
  console.log(stdout);
});
```

传给 `callback` 的 `stdout` 和 `stderr` 包含子进程的输出。
默认情况下，Node.js 会将输出解码成 UTF-8 字符串。
`encoding` 用于指定解码 `stdout` 和 `stderr` 的字符编码。
如果 `encoding` 是 `'buffer'` 或无效的字符编码，则传入 `callback` 的会是 `Buffer`。

如果使用 [`util.promisify()`] 版本的方法，则 `Promise` 返回一个包含 `stdout` 和 `stderr` 的对象。

```js
const util = require('util');
const execFile = util.promisify(require('child_process').execFile);
async function getVersion() {
  const { stdout } = await execFile('node', ['--version']);
  console.log(stdout);
}
getVersion();
```

