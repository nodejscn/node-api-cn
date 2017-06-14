
<!--type=event-->
<!--name=SIGINT, SIGHUP, etc.-->

当Node.js进程接收到一个信号时，会触发信号事件。 signal(7)列出了标准POSIX的信号名称列表，例如`SIGINT`, `SIGHUP`等等。

每个事件名称，以信号名称的大写表示 (比如事件`'SIGINT'` 对应信号 `SIGINT`).

例如:

```js
// Begin reading from stdin so the process does not exit.
process.stdin.resume();

process.on('SIGINT', () => {
  console.log('Received SIGINT.  Press Control-D to exit.');
});
```

*Note*：在大多数终端程序中发送`SIGINT`信号的简单方法是`<Ctrl>-C`。

如下需要重点关注:

* `SIGUSR1` 被Node.js保留用于启动调试器。可以为此事件绑定一个监听器，但是即使这样做也不会阻止调试器的启动。

* `SIGTERM` 和 `SIGINT` 在非windows平台绑定了默认的监听器，这样进程以代码`128 + signal number`结束之前，可以重置终端模式。
  如果这两个事件任意一个绑定了新的监听器，原有默认的行为会被移除(Node.js不会结束)。

* `SIGPIPE` 默认会被忽略。可以给其绑定监听器。

* `SIGHUP` 在Windows平台中当console窗口被关闭时会触发它，在非windows平台中多种相似的条件下也会触发，查看signal(7)。
  可以给其绑定监听器，但是Windows下Node.js会在它触发后10秒钟无条件关闭。
  非windows平台，`SIGHUP`默认的绑定行为是结束Node.js，但是一旦给它绑定了新的监听器，默认行为会被移除。

* `SIGTERM` 在Windows中不支持，可以给其绑定监听器。
* `SIGINT` 在终端运行时，可以被所有平台支持，通常可以通过`CTRL+C`触发(虽然这个不能配置)。
  当终端运行在raw模式，它不会被触发。

* `SIGBREAK` 在Windows中按下`<Ctrl>+<Break>`会被触发，非Windows平台中可以为其绑定监听器，但是没有方式触发或发送此事件。

* `SIGWINCH` 当console被resize时会触发。Windows中只有当光标移动并写入到console，或者以raw模式使用一个可读tty时，才会触发。

* `SIGKILL` 不能绑定监听器，所有平台中出现此事件，都会使得Node.js无条件终止。

* `SIGSTOP` 不能绑定监听器。

* `SIGBUS`, `SIGFPE`, `SIGSEGV` and `SIGILL`, 如果不是通过kill(2)产生，默认会使进程停留在某个状态，在此状态下尝试调用JS监听器是不安全的。
   如果尝试调用JS监听器可能会导致进程在无限循环中挂死，因为使用`process.on()`附加的监听器是以异步的方式被调用，因此不能纠正隐含的问题。

*Note*: Windows不支持发送信号，但是Node.js通过[`process.kill()`][], 和 [`ChildProcess.kill()`][]提供了某些模拟机制。
发送信号`0` 可以测试进程是否存在。发送`SIGINT`, `SIGTERM`, and `SIGKILL` 使得目标进程无条件终止。

