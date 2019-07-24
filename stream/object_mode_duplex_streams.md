
对双工流来说，可以使用 `readableObjectMode` 和 `writableObjectMode` 选项来分别设置可读端和可写端的 `objectMode`。

在下面的例子中，创建了一个变换流（双工流的一种），对象模式的可写端接收 JavaScript 数值，并在可读端转换为十六进制字符串。

```js
const { Transform } = require('stream');

// 转换流也是双工流。
const myTransform = new Transform({
  writableObjectMode: true,

  transform(chunk, encoding, callback) {
    // 强制把 chunk 转换成数值。
    chunk |= 0;

    // 将 chunk 转换成十六进制。
    const data = chunk.toString(16);

    // 推送数据到可读队列。
    callback(null, '0'.repeat(data.length % 2) + data);
  }
});

myTransform.setEncoding('ascii');
myTransform.on('data', (chunk) => console.log(chunk));

myTransform.write(1);
// 打印: 01
myTransform.write(10);
// 打印: 0a
myTransform.write(100);
// 打印: 64
```

