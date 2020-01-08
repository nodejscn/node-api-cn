
* {ArrayBuffer} 创建此 `Buffer` 对象时基于的底层 `ArrayBuffer` 对象。

不能保证此 `ArrayBuffer` 与原始的 `Buffer` 完全对应。 
有关详细信息，参阅 `buf.byteOffset` 上的说明。

```js
const arrayBuffer = new ArrayBuffer(16);
const buffer = Buffer.from(arrayBuffer);

console.log(buffer.buffer === arrayBuffer);
// 打印: true
```

