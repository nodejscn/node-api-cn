<!-- YAML
deprecated: v6.0.0
-->

> 稳定性: 0 - 废弃的: 使用 [`Buffer.from(arrayBuffer[, byteOffset [, length]])`][`Buffer.from(arrayBuffer)`] 代替。

* `arrayBuffer` {ArrayBuffer} An [`ArrayBuffer`] or the `.buffer` property of a
  [`TypedArray`].
* `byteOffset` {Integer} Index of first byte to expose. **Default:** `0`
* `length` {Integer} Number of bytes to expose.
  **Default:** `arrayBuffer.length - byteOffset`

This creates a view of the [`ArrayBuffer`] without copying the underlying
memory. For example, when passed a reference to the `.buffer` property of a
[`TypedArray`] instance, the newly created `Buffer` will share the same
allocated memory as the [`TypedArray`].

The optional `byteOffset` and `length` arguments specify a memory range within
the `arrayBuffer` that will be shared by the `Buffer`.

Example:

```js
const arr = new Uint16Array(2);

arr[0] = 5000;
arr[1] = 4000;

// Shares memory with `arr`
const buf = new Buffer(arr.buffer);

// Prints: <Buffer 88 13 a0 0f>
console.log(buf);

// Changing the original Uint16Array changes the Buffer also
arr[1] = 6000;

// Prints: <Buffer 88 13 70 17>
console.log(buf);
```

