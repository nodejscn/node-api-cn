<!-- YAML
added: v0.7.10
-->

在 Windows 上，设置 `options.detached` 为 `true` 可以使子进程在父进程退出后继续运行。
子进程有自己的控制台窗口。
一旦为子进程启用它，则无法被禁用。

在非 Windows 平台上，如果 `options.detached` 设为 `true`，则子进程会成为新的进程组和会话的主导者。
子进程在父进程退出后可以继续运行，不管它们是否被分离。
详见 setsid(2)。

默认情况下，父进程会等待被分离的子进程退出。
为了防止父进程等待 `subprocess`，可以使用 `subprocess.unref()` 方法。
这样做会使父进程的事件循环不会将子进程包含在其引用计数中，使得父进程可以独立于子进程退出，除非子进程和父进程之间建立了 IPC 通道。

当使用 `detached` 选项来启动长期运行的进程时，该进程在父进程退出后不会保持在后台运行，除非提供不连接到父进程的 `stdio` 配置。
如果父进程的 `stdio` 是继承的，则子进程会保持绑定到控制终端。

示例，一个长期运行的进程，为了忽视父进程的终止，通过分离且忽视其父进程的 `stdio` 文件描述符来实现：

```js
const { spawn } = require('child_process');

const subprocess = spawn(process.argv[0], ['child_program.js'], {
  detached: true,
  stdio: 'ignore'
});

subprocess.unref();
```

也可以重定向子进程的输出到文件：

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

