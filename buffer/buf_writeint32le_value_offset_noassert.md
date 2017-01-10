<!-- YAML
added: v0.5.5
-->

* `value` {Integer} Number to be written to `buf`
* `offset` {Integer} Where to start writing. Must satisfy: `0 <= offset <= buf.length - 4`
* `noAssert` {Boolean} Skip `value` and `offset` validation? **Default:** `false`
* Returns: {Integer} `offset` plus the number of bytes written

Writes `value` to `buf` at the specified `offset` with specified endian
format (`writeInt32BE()` writes big endian, `writeInt32LE()` writes little
endian). `value` *should* be a valid signed 32-bit integer. Behavior is undefined
when `value` is anything other than a signed 32-bit integer.

Setting `noAssert` to `true` allows the encoded form of `value` to extend beyond
the end of `buf`, but the result should be considered undefined behavior.

`value` is interpreted and written as a two's complement signed integer.

Examples:

```js
const buf = Buffer.allocUnsafe(8);

buf.writeInt32BE(0x01020304, 0);
buf.writeInt32LE(0x05060708, 4);

// Prints: <Buffer 01 02 03 04 08 07 06 05>
console.log(buf);
```

