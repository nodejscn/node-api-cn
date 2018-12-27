
* {Stream}

返回连接到 `stdout` (fd `1`) 的流。 
如果 fd `1` 指向文件，则返回[可写流][Writable]，否则返回 [`net.Socket`]（也就是 [Duplex] 流）。

例子，将 `process.stdin` 拷贝到 `process.stdout`：

```js
process.stdin.pipe(process.stdout);
```

`process.stdout` 与其他的 Node.js 流有很大的不同，详见[进程I/O的注意事项][note on process I/O]。

