<!-- YAML
added: v0.7.10
changes:
  - version: v3.3.1
    pr-url: https://github.com/nodejs/node/pull/2727
    description: The value `0` is now accepted as a file descriptor.
-->

`options.stdio` 选项用于配置子进程与父进程之间建立的管道。
默认情况下，子进程的 stdin、 stdout 和 stderr 会重定向到 [`ChildProcess`] 对象上相应的 [`subprocess.stdin`]、 [`subprocess.stdout`] 和 [`subprocess.stderr`] 流。
这等同于将 `options.stdio` 设为 `['pipe', 'pipe', 'pipe']`。

为了方便起见，`options.stdio` 可以是以下字符串之一：

* `'pipe'` - 等同于 `['pipe', 'pipe', 'pipe']` （默认）
* `'ignore'` - 等同于 `['ignore', 'ignore', 'ignore']`
* `'inherit'` - 等同于 `[process.stdin, process.stdout, process.stderr]` 或 `[0,1,2]`

另外，`option.stdio` 的值是一个每个索引都对应一个子进程 fd 的数组。
fd 的 0、1 和 2 分别对应 stdin、stdout 和 stderr。
额外的 fd 可以被指定来创建父进程和子进程之间的额外管道。
该值是以下之一：

1. `'pipe'` - 创建一个子进程和父进程之间的管道。
    在管道的父端以 [`subprocess.stdio[fd]`][`stdio`] 的形式作为 `child_process` 对象的一个属性暴露给父进程。
    为 fd 创建的管道 0 - 2 也可分别作为 [`subprocess.stdin`]、[`subprocess.stdout`] 和 [`subprocess.stderr`]。
2. `'ipc'` - 创建一个用于父进程和子进程之间传递消息或文件描述符的 IPC 通道符。
    一个 [`ChildProcess`] 最多只能有一个 IPC stdio 文件描述符。
    设置该选项可启用 [`subprocess.send()`] 方法。
    如果子进程把 JSON 消息写入到该文件描述符，则 [`subprocess.on('message')`] 事件句柄会被父进程触发。
    如果子进程是一个 Node.js 进程，则一个已存在的 IPC 通道会在子进程中启用 [`process.send()`]、[`process.disconnect()`]、[`process.on('disconnect')`] 和 [`process.on('message')`]。
3. `'ignore'` - 指示 Node.js 在子进程中忽略 fd。
    由于 Node.js 总是会为它衍生的进程打开 fd 0 - 2，所以设置 fd 为 `'ignore'` 可以使 Node.js 打开 `/dev/null` 并将它附加到子进程的 fd 上。
4. {Stream} 对象 - 共享一个指向子进程的 tty、文件、socket 或管道的可读或可写流。
    流的底层文件描述符在子进程中是重复对应该 `stdio` 数组的索引的 fd。
    注意，该流必须有一个底层描述符（文件流直到 `'open'` 事件发生才需要）。
5. 正整数 - 整数值被解析为一个正在父进程中打开的文件描述符。
    它和子进程共享，类似于 {Stream} 是如何被共享的。
6. `null`, `undefined` - 使用默认值。
    对于 stdio fd 0、1 和 2（换言之，stdin、stdout 和 stderr）而言是创建了一个管道。
    对于 fd 3 及以上而言，默认值为 `'ignore'`。

例子：

```js
const { spawn } = require('child_process');

// 子进程使用父进程的 stdios
spawn('prg', [], { stdio: 'inherit' });

// 衍生的子进程只共享 stderr
spawn('prg', [], { stdio: ['pipe', 'pipe', process.stderr] });

// 打开一个额外的 fd=4，用于与程序交互
spawn('prg', [], { stdio: ['pipe', null, null, null, 'pipe'] });
```

当在父进程和子进程之间建立了一个 IPC 通道，且子进程是一个 Node.js 进程，则子进程会带着未引用的 IPC 通道（使用 `unref()`）启动，直到子进程为 [`process.on('disconnect')`] 事件或 [`process.on('message')`] 事件注册了一个事件句柄。
这使得子进程可以在进程没有通过打开的 IPC 通道保持打开的情况下正常退出。

详见 [`child_process.exec()`] 和 [`child_process.fork()`]。

