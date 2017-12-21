
`process.stdout` and `process.stderr` 与 Node.js 中其他 streams 在重要的方面有不同:

1. 他们分别使用内部的 [`console.log()`][] 和 [`console.error()`][]。
2. 他们不能被关闭 (调用[`end()`][]将会抛出异常)。
3. 他们永远不会触发 [`'finish'`][] 事件。
4. 写操作是否为同步，取决于连接的是什么流以及操作系统是 Windows 还是 POSIX :

   - Files: *同步* 在 Windows 和 POSIX 下
   - TTYs (Terminals): *异步* 在 Windows 下， *同步* 在 POSIX 下
   - Pipes (and sockets): *同步* 在 Windows 下， *异步* 在 POSIX 下

这些行为部分是历史原因，改变他们可能导致向后不兼容，而且他们的行为也符合部分用户的预期。

同步写避免了调用 `console.log()` 或 `console.error()` 产生不符合预期的交错输出问题，或是在异步写完成前调用了`process.exit()`导致未写完整。 查看[`process.exit()`][] 获取更多信息。

***警告***: 同步写将会阻塞事件循环直到写完成。 有时可能一瞬间就能写到一个文件，但当系统处于高负载时，管道的接收端可能不会被读取、缓慢的终端或文件系统，因为事件循环被阻塞的足够频繁且足够长的时间，这些可能会给系统性能带来消极的影响。当你向一个交互终端会话写时这可能不是个问题，但当生产日志到进程的输出流时要特别留心。

如果要检查一个流是否连接到了一个 [TTY][] 上下文， 检查 `isTTY` 属性。

例如:
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

查看 [TTY][] 文档以获得更多信息。
