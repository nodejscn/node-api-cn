<!-- YAML
added: v0.7.10
changes:
  - version: v3.3.1
    pr-url: https://github.com/nodejs/node/pull/2727
    description: The value `0` is now accepted as a file descriptor.
-->

用于配置子进程与父进程之间建立的管道。
默认情况下，子进程的 stdin、 stdout 和 stderr 会重定向到 [`ChildProcess`] 对象上相应的 [`subprocess.stdin`]、 [`subprocess.stdout`] 和 [`subprocess.stderr`] 流。
等同于将 `options.stdio` 设为 `['pipe', 'pipe', 'pipe']`。

`options.stdio` 可以是以下字符串之一：

* `'pipe'` - 等同于 `['pipe', 'pipe', 'pipe']`（默认）。
* `'ignore'` - 等同于 `['ignore', 'ignore', 'ignore']`。
* `'inherit'` - 等同于 `['inherit', 'inherit', 'inherit']` 或 `[0,1,2]`。

`option.stdio` 的值是一个数组，其中每个索引对应一个子进程 fd。
fd 的 0、1 和 2 分别对应 stdin、stdout 和 stderr。
额外的 fd 可以指定创建父进程和子进程之间的额外管道。
该值是以下之一：

1. `'pipe'` - 创建一个子进程和父进程之间的管道。
    管道的父端作为 `child_process` 对象的属性。
    为 fd 创建的管道 0 - 2 分别作为 [`subprocess.stdin`]、[`subprocess.stdout`] 和 [`subprocess.stderr`]。
2. `'ipc'` - 创建一个用于父进程和子进程之间传递消息或文件描述符的 IPC 通道符。
    一个 [`ChildProcess`] 最多只能有一个 IPC stdio 文件描述符。
    设置该选项可启用 [`subprocess.send()`]。
    如果子进程是一个 Node.js 进程，则一个已存在的 IPC 通道会在子进程中启用 [`process.send()`] 和 [`process.disconnect()`]，同时也会启用 [`'disconnect'`] 和 [`'message'`] 事件。
3. `'ignore'` - 指示 Node.js 忽略子进程中的 fd。
    由于 Node.js 总是会为它衍生的进程打开 fd 0 - 2，所以设置 fd 为 `'ignore'` 可以使 Node.js 打开 `/dev/null` 并将它附加到子进程的 fd 上。
4. `'inherit'` - 从父进程传入或传入父进程相应的 stdio 流。
    前三个位置分别等同于 `process.stdin`、`process.stdout` 与 `process.stderr`。
    其他位置等同于 `'ignore'`。
5. {Stream} 对象 - 共享一个指向子进程的 tty、文件、socket 或管道的可读或可写流。
    流的底层文件描述符在子进程中对应 `stdio` 数组索引的 fd。
    该流必须有一个底层描述符（文件流直到 `'open'` 事件发生才需要）。
6. 正整数 - 解析成在父进程打开的文件描述符。
    与子进程共享，类似于 Stream 对象的共享。
7. `null` 或 `undefined` - 使用默认值。
    对于 stdio 的 fd 0、1 和 2（换言之，stdin、stdout 和 stderr），创建管道。
    对于 fd 3 及以上，默认为 `'ignore'`。


```js
const { spawn } = require('child_process');

// 子进程使用父进程的 stdio。
spawn('prg', [], { stdio: 'inherit' });

// 衍生的子进程只共享 stderr。
spawn('prg', [], { stdio: ['pipe', 'pipe', process.stderr] });

// 打开一个额外的 fd=4，用于与程序交互。
spawn('prg', [], { stdio: ['pipe', null, null, null, 'pipe'] });
```

