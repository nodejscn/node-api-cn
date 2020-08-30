<!-- YAML
added: v0.7.10
changes:
  - version: v3.3.1
    pr-url: https://github.com/nodejs/node/pull/2727
    description: The value `0` is now accepted as a file descriptor.
-->

`options.stdio` 选项用于配置在父进程和子进程之间建立的管道。
默认情况下，子进程的 stdin、 stdout 和 stderr 会被重定向到 [`ChildProcess`] 对象上相应的 [`subprocess.stdin`]、[`subprocess.stdout`] 和 [`subprocess.stderr`] 流。
这相当于将 `options.stdio` 设置为 `['pipe', 'pipe', 'pipe']`。

为方便起见，`options.stdio` 可以是以下字符串之一：

* `'pipe'` - 相当于 `['pipe', 'pipe', 'pipe']`（默认值）。
* `'ignore'` - 相当于 `['ignore', 'ignore', 'ignore']`。
* `'inherit'` - 相当于 `['inherit', 'inherit', 'inherit']` 或 `[0, 1, 2]`。

否则，`options.stdio` 的值是一个数组，其中每个索引对应于子进程中的 fd。 
fd 0、1 和 2 分别对应于 stdin、stdout 和 stderr。
可以指定其他 fd 以便在父进程和子进程之间创建额外的管道。
值可以是以下之一：

1. `'pipe'` - 在子进程和父进程之间创建一个管道。
    管道的父端作为 `child_process` 对象上的 [`subprocess.stdio[fd]`][`subprocess.stdio`] 属性暴露给父进程。
    为 fd 0 - 2 创建的管道也可分别作为 [`subprocess.stdin`]、[`subprocess.stdout`] 和 [`subprocess.stderr`] 使用。
2. `'ipc'` - 创建一个 IPC 通道，用于在父进程和子进程之间传递消息或文件描述符。 
    一个 [`ChildProcess`] 最多可以有一个 IPC stdio 文件描述符。
    设置此选项会启用 [`subprocess.send()`] 方法。
    如果子进程是一个 Node.js 进程，则 IPC 通道的存在将会启用 [`process.send()`] 和 [`process.disconnect()`] 方法、以及子进程内的 [`'disconnect'`] 和 [`'message'`] 事件。

    以 [`process.send()`] 以外的任何方式访问 IPC 通道的 fd、或者在一个不是 Node.js 实例的子进程中使用 IPC 通道，都是不支持的。
3. `'ignore'` - 指示 Node.js 忽略子进程中的 fd。
    虽然 Node.js 将会始终为它衍生的进程打开 fd 0 - 2，但将 fd 设置为 `'ignore'` 将会导致 Node.js 打开 `/dev/null` 并将其附加到子进程的 fd。
4. `'inherit'` - 将相应的 stdio 流传给父进程或从父进程传入。
    在前三个位置中，这分别相当于 `process.stdin`、`process.stdout` 和 `process.stderr`。
    在任何其他位置中，则相当于 `'ignore'`。
5. {Stream} 对象 - 与子进程共享指向 tty、文件、 socket 或管道的可读或可写流。
    流的底层文件描述符在子进程中会被复制到与 `stdio` 数组中的索引对应的 fd。
    该流必须具有一个底层的描述符（文件流直到触发 `'open'` 事件才有底层文件描述符）。
6. 正整数 - 整数值会被解释为当前在父进程中打开的文件描述符。
    它与子进程共享，类似于共享 {Stream} 对象的方式。
    在 Windows 上不支持传入 socket。
7. `null` 或 `undefined` - 使用默认值。
    对于 stdio 的 fd 0、1 和 2（换句话说，stdin、stdout 和 stderr），将会创建一个管道。
    对于 fd 3 及更大的值，则默认为 `'ignore'`。

```js
const { spawn } = require('child_process');

// 子进程使用父进程的 stdio。
spawn('prg', [], { stdio: 'inherit' });

// 衍生的子进程只共享 stderr。
spawn('prg', [], { stdio: ['pipe', 'pipe', process.stderr] });

// 打开一个额外的 fd=4，与呈现启动式界面的程序进行交互。
spawn('prg', [], { stdio: ['pipe', null, null, null, 'pipe'] });
```

当在父进程和子进程之间建立 IPC 通道，并且子进程是一个 Node.js 进程时，则子进程启动时不会指向 IPC 通道（使用 `unref()`），直到子进程为 [`'disconnect'`] 事件或 [`'message'`] 事件注册了事件处理函数。
这允许子进程正常退出而不需要通过开放的 IPC 通道保持打开该进程。

在类 Unix 操作系统上，[`child_process.spawn()`] 方法在将事件循环与子进程解耦之前会同步地执行内存操作。
具有大内存占用的应用程序可能会发现频繁的 [`child_process.spawn()`] 调用成为瓶颈。
详见 [V8 问题 7381][V8 issue 7381]。

还可参见：[`child_process.exec()`] 和 [`child_process.fork()`]。

