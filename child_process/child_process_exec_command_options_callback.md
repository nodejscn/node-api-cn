<!-- YAML
added: v0.1.90
changes:
  - version: v8.8.0
    pr-url: https://github.com/nodejs/node/pull/15380
    description: The `windowsHide` option is supported now.
-->

* `command` {string} 运行的命令，参数使用空格分隔。
* `options` {Object}
  * `cwd` {string} 子进程的当前工作目录。默认为 `null`。
  * `env` {Object} 环境变量键值对。默认为 `null`。
  * `encoding` {string} 默认为 `'utf8'`。
  * `shell` {string} 执行命令的 shell。参见 [Shell的要求][Shell Requirements]与 [Windows默认的Shell][Default Windows Shell]。
     在 UNIX 上默认为 `'/bin/sh'`，在 Windows 上默认为 `process.env.ComSpec`。
  * `timeout` {number} 默认为 `0`。
  * `maxBuffer` {number} `stdout` 或 `stderr` 允许的最大字节数。如果超过限制，则子进程会终止。参见 [maxBuffer与Unicode][`maxBuffer` and Unicode]。默认为 `200*1024`。
  * `killSignal` {string|integer} 默认为 `'SIGTERM'`。
  * `uid` {number} 进程的用户标识，参见 setuid(2)。
  * `gid` {number} 进程的群组标识，参见 setgid(2)。
  * `windowsHide` {boolean} 是否隐藏子进程的控制台窗口。默认为 `false`。
* `callback` {Function} 当进程终止时调用。
  * `error` {Error}
  * `stdout` {string|Buffer}
  * `stderr` {string|Buffer}
* 返回: {ChildProcess}

衍生一个 shell 并在 shell 中执行 `command`，并缓冲产生的输出。
`command` 会被 shell 直接执行，所以 `command` 中的特殊字符（因[shell](https://en.wikipedia.org/wiki/List_of_command-line_interpreters)而异）需要相应的处理：

```js
exec('"/path/to/test file/test.sh" arg1 arg2');
// 使用双引号，则路径中的空格不会被当成多个参数。

exec('echo "The \\$HOME variable is $HOME"');
// 第一个 $HOME 会被转义，第二个则不会。
```

如果指定了 `callback`，则调用时会传入参数 `(error, stdout, stderr)`。
当成功时，`error` 会是 `null`。
当出错时，`error` 会是 [`Error`] 实例。
`error.code` 属性是子进程的退出码，`error.signal` 是终止进程的信号。
任何非 `0` 的退出码都会被视为出错。

传给 `callback` 的 `stdout` 和 `stderr` 包含子进程的输出。
默认情况下，Node.js 会将输出解码成 UTF-8 字符串。
`encoding` 用于指定解码 `stdout` 和 `stderr` 的字符编码。
如果 `encoding` 是 `'buffer'` 或无效的字符编码，则传入 `callback` 的会是 `Buffer`。

```js
const { exec } = require('child_process');
exec('cat *.js missing_file | wc -l', (error, stdout, stderr) => {
  if (error) {
    console.error(`执行出错: ${error}`);
    return;
  }
  console.log(`stdout: ${stdout}`);
  console.log(`stderr: ${stderr}`);
});
```

如果 `timeout` 大于 `0`，则当子进程运行超过 `timeout` 毫秒时，父进程就会发送带 `killSignal` 属性（默认为 `'SIGTERM'`）的信号。

不像 POSIX 中的 exec(3)， `child_process.exec()` 不会替换现有的进程，且使用 shell 来执行命令。

如果使用 [`util.promisify()`] 版本的方法，则 `Promise` 返回一个包含 `stdout` 和 `stderr` 的对象。

```js
const util = require('util');
const exec = util.promisify(require('child_process').exec);

async function lsExample() {
  const { stdout, stderr } = await exec('ls');
  console.log('stdout:', stdout);
  console.log('stderr:', stderr);
}
lsExample();
```

