
<!--type=event-->
<!--name=SIGINT, SIGHUP, etc.-->

当 Node.js 进程接收到一个信号时，会触发信号事件。 signal(7) 列出了标准POSIX的信号名称列表，例如 `'SIGINT'`、`'SIGHUP'` 等等。

信号在 [`Worker`] 线程上不可用。

信号处理程序将会接收信号的名称（`'SIGINT'`，`'SIGTERM'` 等）作为第一个参数。

每个事件名称，以信号名称的大写表示 (比如事件 `'SIGINT'` 对应信号 `SIGINT`)。

```js
// 从 stdin 开始读取，因此进程不会退出。
process.stdin.resume();

process.on('SIGINT', () => {
  console.log('接收到 SIGINT。 按 Control-D 退出。');
});

// 使用单独的函数处理多个信号。
function handle(signal) {
  console.log(`接收到 ${signal}`);
}

process.on('SIGINT', handle);
process.on('SIGTERM', handle);
```

* `'SIGUSR1'` 被 Node.js 保留用于启动[调试器][debugger]。可以为此事件绑定一个监听器，但是即使这样做也不会阻止调试器的启动。
* `'SIGTERM'` 和 `'SIGINT'` 在非 Windows 平台绑定了默认的监听器，这样进程以代码 `128 + signal number` 结束之前，可以重置终端模式。
  如果这两个事件任意一个绑定了新的监听器，原有默认的行为会被移除（Node.js 不会结束）。
* `'SIGPIPE'` 默认会被忽略。可以给其绑定监听器。
* `'SIGHUP'` 在 Windows 平台中当控制台窗口被关闭时会触发它，在其他平台中多种相似的条件下也会触发，查看 signal(7)。
  可以给其绑定监听器，但是 Windows 下 Node.js 会在它触发后 10 秒钟无条件关闭。
  在非 Windows 平台，`SIGHUP` 默认的绑定行为是结束 Node.js，但是一旦给它绑定了新的监听器，默认行为会被移除。
* `'SIGTERM'` 在 Windows 中不支持，可以给其绑定监听器。
* `'SIGINT'` 在终端运行时，可以被所有平台支持，通常可以通过 `<Ctrl>+C` 触发（虽然这是可以配置的）。
  当终端运行在原始模式，它不会被触发。
* `'SIGBREAK'` 在 Windows 中按下 `<Ctrl>+<Break>` 会被触发，非 Windows 平台中可以为其绑定监听器，但是没有方式触发或发送此事件。
* `'SIGWINCH'` 当控制台被调整大小时会触发。Windows 中只有当光标移动并写入到控制台、或者以原始模式使用一个可读 tty 时，才会触发。
* `'SIGKILL'` 不能绑定监听器，所有平台中出现此事件，都会使得 Node.js 无条件终止。
* `'SIGSTOP'` 不能绑定监听器。
* `'SIGBUS'`、`'SIGFPE'`、`'SIGSEGV'` 和 `'SIGILL'`, 如果不是通过 kill(2) 产生，默认会使进程停留在某个状态，在此状态下尝试调用 JS 监听器是不安全的。
   如果尝试调用 JS 监听器可能会导致进程在无限循环中挂死，因为使用 `process.on()` 附加的监听器是以异步的方式被调用，因此不能纠正隐含的问题。
* 可以发送 `0` 来测试某个进程是否存在，如果该进程存在则没有影响，但是如果该进程不存在则会抛出错误。

Windows 不支持信号，因此没有等效物来通过信号终止，但是 Node.js 提供了一些 [`process.kill()`] 和 [`subprocess.kill()`] 的模拟：


* 发送 `SIGINT`、`SIGTERM` 和 `SIGKILL` 会导致目标进程被无条件地终止，然后子进程会报告该进程已被信号终止。
* 发送信号 `0` 可以用作与平台无关的方式来测试进程的存在性。


