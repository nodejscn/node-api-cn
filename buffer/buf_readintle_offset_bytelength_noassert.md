<!-- YAML
added: v0.11.15
-->

* `offset` {Integer} Where to start reading. Must satisfy: `0 <= offset <= buf.length - byteLength`
* `byteLength` {Integer} How many bytes to read. Must satisfy: `0 < byteLength <= 6`
* `noAssert` {Boolean} Skip `offset` and `byteLength` validation? **Default:** `false`
* Returns: {Integer}

Reads `byteLength` number of bytes from `buf` at the specified `offset`
and interprets the result as a two's complement signed value. Supports up to 48
bits of accuracy.

Setting `noAssert` to `true` allows `offset` to be beyond the end of `buf`, but
the result should be considered undefined behavior.

Examples:

```js
const buf = Buffer.from([0x12, 0x34, 0x56, 0x78, 0x90, 0xab]);

// Prints: 1234567890ab
console.log(buf.readIntLE(0, 6).toString(16));

// Prints: -546f87a9cbee
console.log(buf.readIntBE(0, 6).toString(16));

// Throws an exception: RangeError: Index out of range
console.log(buf.readIntBE(1, 6).toString(16));
```

