
* {Stream}

`process.stdout` 属性会返回连接到 `stdout` (文件描述符 `1`) 的流。
它是一个 [`net.Socket`]（也就是 [Duplex] 流），除非文件描述符 `1` 指向文件（在这种情况下它是一个 [Writable] 流）。

例如，拷贝 `process.stdin` 到 `process.stdout`：

```js
process.stdin.pipe(process.stdout);
```

`process.stdout` 与其他的 Node.js 流有重大区别。
详见[进程 I/O 的注意事项][note on process I/O]。

