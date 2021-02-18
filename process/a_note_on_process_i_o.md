
`process.stdout` 和 `process.stderr` 与其他 Node.js 流有重大不同:

1. 它们分别被用于 [`console.log()`] 和 [`console.error()`] 内部。
2. 写操作是否为同步，取决于连接到的流以及操作系统是 Windows 还是 POSIX：
   * 文件：在 Windows 和 POSIX 上都是同步的。
   * TTY（终端）：在 Windows 上是异步的，在 POSIX 上是同步的。
   * 管道（以及 socket）：在 Windows 上是同步的，在 POSIX 上是异步的。

这些行为部分是历史原因，改变它们可能导致向后不兼容，而且它们的行为也符合部分用户的期望。

同步的写操作可以避免一些问题，比如 `console.log()` 或 `console.error()` 写入的输出被不符合预期地交错，或者在异步的写入完成前调用了 `process.exit()` 导致根本没写入。 
详见 [`process.exit()`]。

注意，同步的写入会阻塞事件循环直到写入完成。 
在输出到文件的情况下，这可能几乎是瞬时的，但当系统处于高负载时，管道的接收端不被读取，或者终端或文件系统速度缓慢，这可能使事件循环经常被长时间阻塞，从而对性能产生严重的负面影响。
当写入到交互的终端会话时，这可能不是个问题，但当写入生产日志到进程的输出流时，则要特别留心。

如果要检查一个流是否连接到了 [TTY] 上下文， 则检查 `isTTY` 属性。

例如：

```console
$ node -p "Boolean(process.stdin.isTTY)"
true
$ echo "foo" | node -p "Boolean(process.stdin.isTTY)"
false
$ node -p "Boolean(process.stdout.isTTY)"
true
$ node -p "Boolean(process.stdout.isTTY)" | cat
false
```

详见 [TTY] 文档。
