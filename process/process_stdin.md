
* {Stream}

`process.stdin` 属性返回连接到 `stdin` (fd `0`) 的流。 
它是一个 [`net.Socket`] 流（也就是[双工流][Duplex]），除非 fd `0` 指向一个文件，在这种情况下它是一个[可读流][Readable]。

```js
process.stdin.setEncoding('utf8');

process.stdin.on('readable', () => {
  const chunk = process.stdin.read();
  if (chunk !== null) {
    process.stdout.write(`数据: ${chunk}`);
  }
});

process.stdin.on('end', () => {
  process.stdout.write('结束');
});
```

作为[双工流][Duplex]，`process.stdin` 也可以在“旧”模式下使用，该模式与在 v0.10 之前为 Node.js 编写的脚本兼容。 
有关更多信息，参阅[流的兼容性][Stream compatibility]。

在“旧”的流模式下，默认情况下 `stdin` 流是暂停的，因此必须调用 `process.stdin.resume()` 从中读取。 
注意，调用 `process.stdin.resume()` 本身会将流切换为“旧”模式。

