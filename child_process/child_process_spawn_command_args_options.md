<!-- YAML
added: v0.1.90
changes:
  - version: v8.8.0
    pr-url: https://github.com/nodejs/node/pull/15380
    description: The `windowsHide` option is supported now.
  - version: v6.4.0
    pr-url: https://github.com/nodejs/node/pull/7696
    description: The `argv0` option is supported now.
  - version: v5.7.0
    pr-url: https://github.com/nodejs/node/pull/4598
    description: The `shell` option is supported now.
-->

* `command` {string} 运行的命令。
* `args` {string[]} 参数列表。
* `options` {Object}
  * `cwd` {string} 子进程的当前工作目录。
  * `env` {Object} 环境变量键值对。
  * `argv0` {string} 发送给子进程的 `argv[0]` 的值。如果没有指定，则设为 `command` 的值。
  * `stdio` {Array|string} 子进程的 stdio 配置。参见 [`options.stdio`][`stdio`]。
  * `detached` {boolean} 子进程是否独立于父进程运行。参见 [`options.detached`]。
  * `uid` {number} 进程的用户标识。参见 setuid(2)。
  * `gid` {number} 进程的群组标识。参见 setgid(2)。
  * `shell` {boolean|string} 如果设为 `true`，则在 shell 中运行 `command`。
     在 UNIX 上使用 `'/bin/sh'`，在 Windows 上使用 `process.env.ComSpec`。
     传入字符串则指定其他 `shell`。
     参见 [Shell的要求][Shell Requirements]与 [Windows默认的Shell][Default Windows Shell]。
     默认为 `false`（没有 shell）。
  * `windowsVerbatimArguments` {boolean} 在 Windows 上是否为参数加引号或转义。如果指定了 `shell`，则自动设为 `true`。默认为 `false`。
  * `windowsHide` {boolean} 是否隐藏子进程的控制台窗口。默认为 `false`。
* 返回: {ChildProcess}

使用 `command` 和 `args` 衍生进程。

`options` 可以指定额外的选项，默认如下：

```js
const defaults = {
  cwd: undefined,
  env: process.env
};
```

`cwd` 指定衍生的进程的工作目录。
如果没有指定，则默认为当前工作目录。

`env` 指定环境变量，默认为 [`process.env`]。

`env` 中值为 `undefined` 的属性会被忽略。

例子，运行 `ls -lh /usr`，并捕获 `stdout`、`stderr`、以及退出码：

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

例子，运行 `ps ax | grep ssh`：

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
  console.log('启动子进程失败');
});
```

在 macOS 和 Linux 上会使用 `argv[0]` 的值作为进程的标题，而在 Windows 和 SunOS 上则使用 `command` 作为标题。

Node.js 一般会在启动时用 `process.execPath` 重写 `argv[0]`，所以子进程的 `process.argv[0]` 不会匹配从父进程传给 `spawn` 的 `argv0`，可以使用 `process.argv0` 获取。

