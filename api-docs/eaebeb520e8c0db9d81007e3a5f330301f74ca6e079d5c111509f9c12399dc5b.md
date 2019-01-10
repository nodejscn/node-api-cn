
* {Stream}

返回连接到 `stdin` (fd `0`) 的流。 
如果 fd `0` 指向文件，则返回[可读流][Readable]，否则返回 [`net.Socket`]（也就是 [Duplex] 流）。

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

如果 `process.stdin` 返回的是 [Duplex] 流, 也可以在兼容 Node.js v0.10 之前版本的旧模式中使用。
详见[流的兼容性][Stream compatibility]。

