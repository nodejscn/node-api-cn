
<!--type=event-->
<!--name=SIGINT, SIGHUP, etc.-->

当 Node.js 进程接收到信号时，则会触发信号事件。 
signal(7) 文档可查看标准 POSIX 的信号名称的列表，例如 `'SIGINT'`、`'SIGHUP'` 等。

信号在 [`Worker`] 线程上不可用。

信号句柄会接收信号的名称（`'SIGINT'`，`'SIGTERM'` 等）作为第一个参数。

每个事件的名称是信号的通用名称的大写 (比如 `'SIGINT'` 事件对应 `SIGINT` 信号)。

```js
// 开始从 stdin 读取，因此进程不会退出。
process.stdin.resume();

process.on('SIGINT', () => {
  console.log('接收到 SIGINT。按 Control-D 退出。');
});

// 使用单独的函数处理多个信号。
function handle(signal) {
  console.log(`接收到 ${signal}`);
}

process.on('SIGINT', handle);
process.on('SIGTERM', handle);
```

* `'SIGUSR1'` 被 Node.js 保留用于启动[调试器][debugger]。
  可以为此事件绑定监听器，但是即使这样做也不会阻止调试器的启动。
* `'SIGTERM'` 和 `'SIGINT'` 在非 Windows 平台具有默认的句柄（在以退出码 `128 + 信号数字` 退出之前，会重置终端模式）。
  如果任一事件绑定了监听器，则其默认的行为会被移除（Node.js 不再会退出）。
* `'SIGPIPE'` 默认会被忽略。
  可以给其绑定监听器。
* `'SIGHUP'` 在 Windows 平台上当控制台窗口被关闭时会触发，在其他平台上在多种相似的条件下也会触发，详见 signal(7)。
  可以给其绑定监听器，但是 Windows 上 Node.js 会在触发后 10 秒后被无条件地终止。
  在非 Windows 平台上，`SIGHUP` 的默认行为是终止 Node.js，但是一旦绑定了监听器，则默认的行为会被移除。
* `'SIGTERM'` 在 Windows 上不支持，可以为其绑定监听器。
* `'SIGINT'` 从终端运行时，所有平台上都支持，通常可以使用 <kbd>Ctrl</kbd>+<kbd>C</kbd>（但是这是可以配置的）触发。
  当启用[终端的原始模式][terminal raw mode]时，则使用 <kbd>Ctrl</kbd>+<kbd>C</kbd> 不会触发。
* `'SIGBREAK'` 在 Windows 上，当按下 <kbd>Ctrl</kbd>+<kbd>Break</kbd> 时则会触发。
  在非 Windows 平台上，可以为其绑定监听器，但是无法发送或触发此事件。
* `'SIGWINCH'` 当控制台被调整大小时则会触发。
  在 Windows 上，只有当写入控制台时移动光标、或者在原始模式中使用可读的 tty 时，才会触发。
* `'SIGKILL'` 不能绑定监听器，在所有平台上，都会无条件地终止 Node.js。
* `'SIGSTOP'` 不能绑定监听器。
* `'SIGBUS'`、`'SIGFPE'`、`'SIGSEGV'` 和 `'SIGILL'`, 如果不是使用 kill(2) 产生，则默认会使进程停留在某种状态（在此状态下调用 JS 监听器是不安全的）。
   这样做可能会导致进程停止响应。
* 可以发送 `0` 来测试进程是否存在，如果该进程存在则没有影响，但是如果该进程不存在则会抛出错误。

Windows 不支持信号，因此没有等效物来通过信号终止，但是 Node.js 提供了一些 [`process.kill()`] 和 [`subprocess.kill()`] 的模拟：
* 发送 `SIGINT`、`SIGTERM` 和 `SIGKILL` 会使目标进程被无条件地终止，然后子进程会报告该进程已被信号终止。
* 发送信号 `0` 可以用作与平台无关的方式来测试进程的存在性。


