<!-- YAML
added: v0.1.90
-->

* `command` {string} 要运行的命令，用空格分隔参数
* `options` {Object}
  * `cwd` {string} 子进程的当前工作目录
  * `env` {Object} 环境变量键值对
  * `encoding` {string} （默认: `'utf8'`）
  * `shell` {string} 用于执行命令的 shell
    （默认：在 UNIX 上为 `'/bin/sh'`，在 Windows 上为 `process.env.ComSpec`。
    See [Shell Requirements][] and [Default Windows Shell][].）
  * `timeout` {number} （默认: `0`）
  * [`maxBuffer`] {number} stdout 或 stderr 允许的最大字节数。
    默认为 `200*1024`。
    如果超过限制，则子进程会被终止。
    查看警告： [`maxBuffer` and Unicode][].
  * `killSignal` {string|integer} （默认: `'SIGTERM'`）
  * `uid` {number} 设置该进程的用户标识。（详见 setuid(2)）
  * `gid` {number} 设置该进程的组标识。（详见 setgid(2)）
* `callback` {Function} 当进程终止时调用，并带上输出。
  * `error` {Error}
  * `stdout` {string|Buffer}
  * `stderr` {string|Buffer}
* 返回: {ChildProcess}

衍生一个 shell，然后在 shell 中执行 `command`，且缓冲任何产生的输出。传入 exec  函数的 `command` 字符串会被 shell 直接处理，特殊字符（因 [shell](https://en.wikipedia.org/wiki/List_of_command-line_interpreters) 而异）需要相应处理：

```js
exec('"/path/to/test file/test.sh" arg1 arg2');
// 使用双引号这样路径中的空格就不会被解释为多个参数

exec('echo "The \\$HOME variable is $HOME"');
// 第一个 $HOME 被转义了，但第二个没有
```

注意：不要把未经检查的用户输入传入到该函数。
任何包括 shell 元字符的输入都可被用于触发任何命令的执行。

```js
const { exec } = require('child_process');
exec('cat *.js bad_file | wc -l', (error, stdout, stderr) => {
  if (error) {
    console.error(`exec error: ${error}`);
    return;
  }
  console.log(`stdout: ${stdout}`);
  console.log(`stderr: ${stderr}`);
});
```

如果提供了一个 `callback` 函数，则它被调用时会带上参数 `(error, stdout, stderr)`。
当成功时，`error` 会是 `null`。
当失败时，`error` 会是一个 [`Error`] 实例。
`error.code` 属性会是子进程的退出码，`error.signal` 会被设为终止进程的信号。
除 `0` 以外的任何退出码都被认为是一个错误。

传给回调的 `stdout` 和 `stderr` 参数会包含子进程的 stdout 和 stderr 的输出。
默认情况下，Node.js 会解码输出为 UTF-8，并将字符串传给回调。
`encoding` 选项可用于指定用于解码 stdout 和 stderr 输出的字符编码。
如果 `encoding` 是 `'buffer'`、或一个无法识别的字符编码，则传入 `Buffer` 对象到回调函数。

`options` 参数可以作为第二个参数传入，用于自定义如何衍生进程。
默认的选项是：

```js
const defaults = {
  encoding: 'utf8',
  timeout: 0,
  maxBuffer: 200 * 1024,
  killSignal: 'SIGTERM',
  cwd: null,
  env: null
};
```

如果 `timeout` 大于 `0`，当子进程运行超过 `timeout` 毫秒时，父进程就会发送由 `killSignal` 属性标识的信号（默认为 `'SIGTERM'`）。

注意：不像 POSIX 系统调用中的 exec(3)，`child_process.exec()` 不会替换现有的进程，且使用一个 shell 来执行命令。

如果调用该方法的 [`util.promisify()`][] 版本，将会返回一个包含 `stdout` 和 `stderr` 的 Promise 对象。在出现错误的情况洗，将返回 rejected 状态的 promise，拥有与回调函数一样的 `error` 对象，但附加了 `stdout` 和 `stderr` 属性。

例子:

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
