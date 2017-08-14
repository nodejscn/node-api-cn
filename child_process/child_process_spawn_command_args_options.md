<!-- YAML
added: v0.1.90
changes:
  - version: v6.4.0
    pr-url: https://github.com/nodejs/node/pull/7696
    description: The `argv0` option is supported now.
  - version: v5.7.0
    pr-url: https://github.com/nodejs/node/pull/4598
    description: The `shell` option is supported now.
-->

* `command` {string} 要运行的命令
* `args` {Array} 字符串参数列表
* `options` {Object}
  * `cwd` {string} 子进程的当前工作目录
  * `env` {Object} 环境变量键值对
  * `argv0` {string} 显式地设置要发给子进程的 `argv[0]` 的值。
    如果未指定，则设为 `command`。
  * `stdio` {Array|string} 子进程的 stdio 配置。
    （详见 [`options.stdio`]）
  * `detached` {boolean} 准备将子进程独立于父进程运行。
    具体行为取决于平台。（详见 [`options.detached`]）
  * `uid` {number} 设置该进程的用户标识。（详见 setuid(2)）
  * `gid` {number} 设置该进程的组标识。（详见 setgid(2)）
  * `shell` {boolean|string} 如果为 `true`，则在一个 shell 中运行 `command`。
    在 UNIX 上使用 `'/bin/sh'`，在 Windows 上使用 `process.env.ComSpec`。
    一个不同的 shell 可以被指定为字符串。
    See [Shell Requirements][] and [Default Windows Shell][].
    默认为 `false`（没有 shell）。
* 返回: {ChildProcess}

`child_process.spawn()` 方法使用给定的 `command` 和 `args` 中的命令行参数来衍生一个新进程。
如果省略 `args`，则默认为一个空数组。

注意：不要把未经检查的用户输入传入到该函数。
任何包括 shell 元字符的输入都可被用于触发任何命令的执行。

第三个参数可以用来指定额外的选项，默认如下：

```js
const defaults = {
  cwd: undefined,
  env: process.env
};
```

使用 `cwd` 来指定衍生的进程的工作目录。
如果没有给出，则默认继承当前的工作目录。

使用 `env` 来指定环境变量，这会在新进程中可见，默认为 [`process.env`]。

例子，运行 `ls -lh /usr`，捕获 `stdout`、`stderr`、以及退出码：

```js
const { spawn } = require('child_process');
const ls = spawn('ls', ['-lh', '/usr']);

ls.stdout.on('data', (data) => {
  console.log(`stdout: ${data}`);
});

ls.stderr.on('data', (data) => {
  console.log(`stderr: ${data}`);
});

ls.on('close', (code) => {
  console.log(`子进程退出码：${code}`);
});
```

例子，一种执行 `'ps ax | grep ssh'` 的方法：

```js
const { spawn } = require('child_process');
const ps = spawn('ps', ['ax']);
const grep = spawn('grep', ['ssh']);

ps.stdout.on('data', (data) => {
  grep.stdin.write(data);
});

ps.stderr.on('data', (data) => {
  console.log(`ps stderr: ${data}`);
});

ps.on('close', (code) => {
  if (code !== 0) {
    console.log(`ps 进程退出码：${code}`);
  }
  grep.stdin.end();
});

grep.stdout.on('data', (data) => {
  console.log(data.toString());
});

grep.stderr.on('data', (data) => {
  console.log(`grep stderr: ${data}`);
});

grep.on('close', (code) => {
  if (code !== 0) {
    console.log(`grep 进程退出码：${code}`);
  }
});
```

例子，检测失败的 `spawn`：

```js
const { spawn } = require('child_process');
const subprocess = spawn('bad_command');

subprocess.on('error', (err) => {
  console.log('启动子进程失败。');
});
```

注意：某些平台（macOS, Linux）会使用 `argv[0]` 的值作为进程的标题，而其他平台（Windows, SunOS）则使用 `command`。

注意，Node.js 一般会在启动时用 `process.execPath` 重写 `argv[0]`，所以 Node.js 子进程中的 `process.argv[0]` 不会匹配从父进程传给 `spawn` 的 `argv0` 参数，可以使用 `process.argv0` 属性获取它。

