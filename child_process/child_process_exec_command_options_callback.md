<!-- YAML
added: v0.1.90
changes:
  - version: v8.8.0
    pr-url: https://github.com/nodejs/node/pull/15380
    description: 支持 `windowsHide` 选项。
-->

* `command` {string} 要运行的命令，参数使用空格分隔。
* `options` {Object}
  * `cwd` {string} 子进程的当前工作目录。
    **默认值:** `null`。
  * `env` {Object} 环境变量的键值对。
    **默认值:** `process.env`。
  * `encoding` {string} **默认值:** `'utf8'`。
  * `shell` {string} 用于执行命令。
    参见 [shell 的要求][Shell Requirements]和[默认的 Windows shell][Default Windows Shell]。
     **默认值:** Unix 上是 `'/bin/sh'`，Windows 上是 `process.env.ComSpec`。
  * `timeout` {number} **默认值:** `0`。
  * `maxBuffer` {number} stdout 或 stderr 上允许的最大数据量（以字节为单位）。
    如果超过限制，则子进程会被终止，并且输出会被截断。
    参见 [maxBuffer 和 Unicode][`maxBuffer` and Unicode] 的注意事项。
    **默认值:** `1024 * 1024`。
  * `killSignal` {string|integer} **默认值:** `'SIGTERM'`。
  * `uid` {number} 设置进程的用户标识，参见 setuid(2)。
  * `gid` {number} 设置进程的群组标识，参见 setgid(2)。
  * `windowsHide` {boolean} 隐藏子进程的控制台窗口（在 Windows 系统上通常会创建）。
    **默认值:** `false`。
* `callback` {Function} 当进程终止时调用并传入输出。
  * `error` {Error}
  * `stdout` {string|Buffer}
  * `stderr` {string|Buffer}
* 返回: {ChildProcess}

衍生 shell，然后在 shell 中执行 `command`，并缓冲任何产生的输出。
传给 exec 函数的 `command` 字符串会被 shell 直接处理，特殊字符（因 [shell][shell special characters] 而异）需要被相应地处理：

```js
exec('"/目录/空 格/文件.sh" 参数1 参数2');
// 使用双引号，使路径中的空格不会被解释为多个参数的分隔符。

exec('echo "\\$HOME 变量为 $HOME"');
// $HOME 变量在第一个实例中会被转义，但是第二个则不会。
```

**切勿将未经过处理的用户输入传给此函数。
包含 shell 元字符的任何输入都可用于触发任意命令的执行。**

如果提供了 `callback` 函数，则调用时会传入参数 `(error, stdout, stderr)`。
当成功时，则 `error` 会为 `null`。
当报错时，则 `error` 会是 [`Error`] 的实例。
`error.code` 属性是子进程的退出码，`error.signal` 会被设为终止进程的信号。
除 `0` 以外的任何退出码都会被视为错误。

传给回调的 `stdout` 和 `stderr` 参数会包含子进程的 stdout 和 stderr 输出。
默认情况下，Node.js 会将输出解码为 UTF-8 并将字符串传给回调。
`encoding` 选项可用于指定字符编码（用于解码 stdout 和 stderr 输出）。
如果 `encoding` 是 `'buffer'` 或无法识别的字符编码，则传给回调的会是 `Buffer` 对象。

```js
const { exec } = require('child_process');
exec('cat *.js 文件 | wc -l', (error, stdout, stderr) => {
  if (error) {
    console.error(`执行的错误: ${error}`);
    return;
  }
  console.log(`stdout: ${stdout}`);
  console.error(`stderr: ${stderr}`);
});
```

如果 `timeout` 大于 `0`，则当子进程运行时间超过 `timeout` 毫秒时，父进程会发送由 `killSignal` 属性（默认为 `'SIGTERM'`）标识的信号。

与 exec(3) 的 POSIX 系统调用不同，`child_process.exec()` 不会替换现有的进程，而是使用 shell 来执行命令。

如果调用此方法的 [`util.promisify()`] 版本，则返回 `Promise`（会传入具有 `stdout` 和 `stderr` 属性的 `Object`）。
返回的 `ChildProcess` 实例会作为 `child` 属性附加到 `Promise`。
如果出现错误（包括导致退出码不为 0 的任何错误），则返回 reject 的 promise，并传入与回调中相同的 `error` 对象，但是还有两个额外的属性 `stdout` 和 `stderr`。

```js
const util = require('util');
const exec = util.promisify(require('child_process').exec);

async function lsExample() {
  const { stdout, stderr } = await exec('ls');
  console.log('stdout:', stdout);
  console.error('stderr:', stderr);
}
lsExample();
```

