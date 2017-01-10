<!-- YAML
added: v0.5.0
-->

* `value` {Integer} Number to be written to `buf`
* `offset` {Integer} Where to start writing. Must satisfy: `0 <= offset <= buf.length - 1`
* `noAssert` {Boolean} Skip `value` and `offset` validation? **Default:** `false`
* Returns: {Integer} `offset` plus the number of bytes written

Writes `value` to `buf` at the specified `offset`. `value` *should* be a
valid unsigned 8-bit integer. Behavior is undefined when `value` is anything
other than an unsigned 8-bit integer.

Setting `noAssert` to `true` allows the encoded form of `value` to extend beyond
the end of `buf`, but the result should be considered undefined behavior.

Examples:

```js
const buf = Buffer.allocUnsafe(4);

buf.writeUInt8(0x3, 0);
buf.writeUInt8(0x4, 1);
buf.writeUInt8(0x23, 2);
buf.writeUInt8(0x42, 3);

// Prints: <Buffer 03 04 23 42>
console.log(buf);
```

