<!-- YAML
deprecated: v6.0.0
-->

> Stability: 0 - Deprecated: Use
> [`Buffer.from(arrayBuffer[, byteOffset [, length]])`][`Buffer.from(arrayBuffer)`]
> instead.

* `arrayBuffer` {ArrayBuffer} The `.buffer` property of a [`TypedArray`] or
  [`ArrayBuffer`]
* `byteOffset` {Integer} Where to start copying from `arrayBuffer`. **Default:** `0`
* `length` {Integer} How many bytes to copy from `arrayBuffer`.
  **Default:** `arrayBuffer.length - byteOffset`

When passed a reference to the `.buffer` property of a [`TypedArray`] instance,
the newly created `Buffer` will share the same allocated memory as the
[`TypedArray`].

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

