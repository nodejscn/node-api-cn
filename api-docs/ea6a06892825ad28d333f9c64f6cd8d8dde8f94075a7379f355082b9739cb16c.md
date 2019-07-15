
* {ArrayBuffer} 创建 `Buffer` 对象时基于的底层 `ArrayBuffer` 对象。

```js
const arrayBuffer = new ArrayBuffer(16);
const buffer = Buffer.from(arrayBuffer);

console.log(buffer.buffer === arrayBuffer);
// 打印: true
```

