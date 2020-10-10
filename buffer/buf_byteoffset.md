
* {integer} `Buffer` 底层的 `ArrayBuffer` 对象的 `byteOffset`。

当 `Buffer.from(ArrayBuffer, byteOffset, length)` 设置了 `byteOffset` 或创建一个小于 `Buffer.poolSize` 的 `Buffer` 时，底层的 `ArrayBuffer` 的偏移量并不是从 0 开始。

当直接使用 `buf.buffer` 访问底层的 `ArrayBuffer` 时可能会导致问题，因为 `ArrayBuffer` 的其他部分可能并不指向 `Buffer` 对象。

当创建与 `Buffer` 共享其内存的 `TypedArray` 对象时，需要正确地指定 `byteOffset`。

```js
// 创建一个小于 `Buffer.poolSize` 的 buffer。
const nodeBuffer = new Buffer.from([0, 1, 2, 3, 4, 5, 6, 7, 8, 9]);

// 当将 Node.js Buffer 转换为 Int8Array 时，
// 应使用 byteOffset 仅引用 `nodeBuffer.buffer` 中包含 `nodeBuffer` 内存的部分。
new Int8Array(nodeBuffer.buffer, nodeBuffer.byteOffset, nodeBuffer.length);
```

