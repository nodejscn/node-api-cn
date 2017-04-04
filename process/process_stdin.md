
* {Stream}

执行`process.stdin` 会返回一个 [可读流]，等同于 `stdin` (fd `0`).

举个例子:

```js
process.stdin.setEncoding('utf8');

process.stdin.on('readable', () => {
  var chunk = process.stdin.read();
  if (chunk !== null) {
    process.stdout.write(`data: ${chunk}`);
  }
});

process.stdin.on('end', () => {
  process.stdout.write('end');
});
```

`process.stdin` 返回的 [可读流], 可以在`旧`模式下使用,兼容node v0.10。
更多信息查看[流的兼容性]。

*注意*: 在"旧模式下" `stdin`流 默认是暂停的.所以必须通过执行`.stdin.resume()`来恢复它.
同时`process.stdin.resume()`会切换到`旧模式`
