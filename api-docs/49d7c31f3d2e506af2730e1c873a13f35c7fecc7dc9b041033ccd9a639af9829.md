<!-- YAML
added: v0.9.4
-->

* `destination` {stream.Writable} 要移除管道的可写流。
* 返回: {this}

解绑之前使用 [`stream.pipe()`] 绑定的可写流。

如果没有指定 `destination`, 则解绑所有管道.

如果指定了 `destination`, 但它没有建立管道，则不起作用.

```js
const fs = require('fs');
const readable = getReadableStreamSomehow();
const writable = fs.createWriteStream('file.txt');
// 可读流的所有数据开始传输到 'file.txt'，但一秒后停止。
readable.pipe(writable);
setTimeout(() => {
  console.log('停止写入 file.txt');
  readable.unpipe(writable);
  console.log('手动关闭文件流');
  writable.end();
}, 1000);
```

