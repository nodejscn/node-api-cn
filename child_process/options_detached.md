<!-- YAML
added: v0.7.10
-->

在 Windows 上，设置 `options.detached` 为 `true` 可以使子进程在父进程退出后继续运行。
子进程有自己的控制台窗口。
一旦启用一个子进程，它将不能被禁用。

在非 Windows 平台上，如果将 `options.detached` 设为 `true`，则子进程会成为新的进程组和会话的领导者。
注意，子进程在父进程退出后可以继续运行，不管它们是否被分离。
详见 setsid(2)。

默认情况下，父进程会等待被分离的子进程退出。
为了防止父进程等待给定的 `subprocess`，可以使用 `subprocess.unref()` 方法。
这样做会导致父进程的事件循环不包含子进程的引用计数，使得父进程独立于子进程退出，除非子进程和父进程之间建立了一个 IPC 信道。

当使用 `detached` 选项来启动一个长期运行的进程时，该进程不会在父进程退出后保持在后台运行，除非提供了一个不连接到父进程的 `stdio` 配置。
如果父进程的 `stdio` 是继承的，则子进程会保持连接到控制终端。

例子，一个长期运行的进程，为了忽视父进程的终止，通过分离且忽视其父进程的 `stdio` 文件描述符来实现：

```js
const { spawn } = require('child_process');

const subprocess = spawn(process.argv[0], ['child_program.js'], {
  detached: true,
  stdio: 'ignore'
});

subprocess.unref();
```

也可以将子进程的输出重定向到文件：

```js
const fs = require('fs');
const { spawn } = require('child_process');
const out = fs.openSync('./out.log', 'a');
const err = fs.openSync('./out.log', 'a');

const subprocess = spawn('prg', [], {
  detached: true,
  stdio: [ 'ignore', out, err ]
});

subprocess.unref();
```

