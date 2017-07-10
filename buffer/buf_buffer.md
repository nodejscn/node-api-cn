
`buffer` 属性指向创建该 `Buffer` 的底层的 `ArrayBuffer` 对象。

```js
const arrayBuffer = new ArrayBuffer(16);
const buffer = Buffer.from(arrayBuffer);

console.log(buffer.buffer === arrayBuffer);
// 输出: true
```
