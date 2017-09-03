
* {Stream}

The `process.stdin` property returns a stream connected to
`stdin` (fd `0`). It is a [`net.Socket`][] (which is a [Duplex][]
stream) unless fd `0` refers to a file, in which case it is
a [Readable][] stream.

`process.stdin` 属性返回连接到`stdin`(fd `0`)的流。 
它是一个[`net.Socket`][](它是一个[Duplex][]流)，除非 fd `0`指向一个文件，在这种情况下它是一个[可读][]流。

举个例子:

```js
process.stdin.setEncoding('utf8');

process.stdin.on('readable', () => {
  const chunk = process.stdin.read();
  if (chunk !== null) {
    process.stdout.write(`data: ${chunk}`);
  }
});

process.stdin.on('end', () => {
  process.stdout.write('end');
});
```

`process.stdin` 返回的 [Duplex] 流, 可以在`旧`模式下使用,兼容node v0.10。
更多信息查看[流的兼容性]。

*注意*: 在"旧模式下" `stdin`流 默认是暂停的.所以必须通过执行`.stdin.resume()`来恢复它.
同时`process.stdin.resume()`会切换到`旧模式`
