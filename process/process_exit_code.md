<!-- YAML
added: v0.1.13
-->

* `code` {integer} 退出码。**默认值:** `0`。

`process.exit()` 方法以退出状态 `code` 指示 Node.js 同步地终止进程。
如果省略 `code`，则使用成功代码 `0` 或 `process.exitCode` 的值（如果已设置）退出。
在所有的 [`'exit'`] 事件监听器被调用之前，Node.js 不会终止。

使用失败代码退出：

```js
process.exit(1);
```

执行 Node.js 的 shell 可以看到退出码为 `1`。

调用 `process.exit()` 会强制进程尽快退出，即使还有尚未完全完成的异步操作在等待，包括对 `process.stdout` 和 `process.stderr` 的 I/O 操作。

在大多数情况下，实际上不需要显式地调用 `process.exit()`。
如果事件循环中没有待处理的额外工作，则 Node.js 进程会自行退出。 
`process.exitCode` 属性可以设置来告诉进程使用什么退出码（当进程正常退出时）。

例如，以下示例描述了 `process.exit()` 方法的错误用法，这可能会导致打印到 stdout 的数据被截断和丢失：

```js
// 这是一个错误用法的示例：
if (someConditionNotMet()) {
  printUsageToStdout();
  process.exit(1);
}
```

这个问题的原因是因为 Node.js 中的 `process.stdout` 的写入有时是异步的，并且可能发生在 Node.js 事件循环的多个时间点。
但是，调用 `process.exit()` 会强制进程退出（在这些额外的 `stdout` 写入操作被执行之前）。

代码不应直接调用 `process.exit()`，而应设置 `process.exitCode` 并允许进程自然地退出（避免为事件循环调度任何额外的工作）：

```js
// 如何正确地设置退出码，同时让进程正常地退出。
if (someConditionNotMet()) {
  printUsageToStdout();
  process.exitCode = 1;
}
```

如果由于错误条件而需要终止 Node.js 进程，则抛出未捕获的错误并允许进程相应地终止，这比调用 `process.exit()` 更安全。

在 [`Worker`] 线程中，此函数会停止当前线程（而不是当前进程）。


