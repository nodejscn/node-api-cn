
* {integer} The `byteOffset` on the underlying `ArrayBuffer` object based on
  which this `Buffer` object is created.

When setting `byteOffset` in `Buffer.from(ArrayBuffer, byteOffset, length)`
or sometimes when allocating a buffer smaller than `Buffer.poolSize` the
buffer doesn't start from a zero offset on the underlying `ArrayBuffer`.

This can cause problems when accessing the underlying `ArrayBuffer` directly
using `buf.buffer`, as the first bytes in this `ArrayBuffer` may be unrelated
to the `buf` object itself.

A common issue is when casting a `Buffer` object to a `TypedArray` object,
in this case one needs to specify the `byteOffset` correctly:

```js
// Create a buffer smaller than `Buffer.poolSize`.
const nodeBuffer = new Buffer.from([0, 1, 2, 3, 4, 5, 6, 7, 8, 9]);

// When casting the Node.js Buffer to an Int8 TypedArray remember to use the
// byteOffset.
new Int8Array(nodeBuffer.buffer, nodeBuffer.byteOffset, nodeBuffer.length);
```

