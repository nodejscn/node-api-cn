<!-- YAML
added: v0.1.91
-->

* `file` {string} 要运行的可执行文件的名称或路径
* `args` {Array} 字符串参数列表
* `options` {Object}
  * `cwd` {string} 子进程的当前工作目录
  * `env` {Object} 环境变量键值对
  * `encoding` {string} （默认: `'utf8'`）
  * `timeout` {number} （默认: `0`）
  * [`maxBuffer`] {number} stdout 或 stderr 允许的最大字节数。
    默认为 `200*1024`。
    如果超过限制，则子进程会被终止。
    See caveat at [`maxBuffer` and Unicode][].
  * `killSignal` {string|integer} （默认: `'SIGTERM'`）
  * `uid` {number} 设置该进程的用户标识。（详见 setuid(2)）
  * `gid` {number} 设置该进程的组标识。（详见 setgid(2)）
* `callback` {Function} 当进程终止时调用，并带上输出。
  * `error` {Error}
  * `stdout` {string|Buffer}
  * `stderr` {string|Buffer}
* 返回: {ChildProcess}

`child_process.execFile()` 函数类似 [`child_process.exec()`]，除了不衍生一个 shell。
而是，指定的可执行的 `file` 被直接衍生为一个新进程，这使得它比 [`child_process.exec()`] 更高效。

它支持和 [`child_process.exec()`] 一样的选项。
由于没有衍生 shell，因此不支持像 I/O 重定向和文件查找这样的行为。

```js
const { execFile } = require('child_process');
const child = execFile('node', ['--version'], (error, stdout, stderr) => {
  if (error) {
    throw error;
  }
  console.log(stdout);
});
```

传给回调的 `stdout` 和 `stderr` 参数会包含子进程的 stdout 和 stderr 的输出。
默认情况下，Node.js 会解码输出为 UTF-8，并将字符串传给回调。
`encoding` 选项可用于指定用于解码 stdout 和 stderr 输出的字符编码。
如果 `encoding` 是 `'buffer'`、或一个无法识别的字符编码，则传入 `Buffer` 对象到回调函数。

如果调用该方法的 [`util.promisify()`][] 版本， 它会返回一个拥有 `stdout` 和
`stderr` 属性的 Promise 对象. 在发生错误的情况下, 返回一个 rejected 状态的 promise, 拥有与回调
函数一样的 `error` 对象, 但是附加了 `stdout` 和 `stderr` 这两个属性.

```js
const util = require('util');
const execFile = util.promisify(require('child_process').execFile);
async function getVersion() {
  const { stdout } = await execFile('node', ['--version']);
  console.log(stdout);
}
getVersion();
```
