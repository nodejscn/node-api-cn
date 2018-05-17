<!-- YAML
added: v0.11.15
changes:
  - version: v10.0.0
    pr-url: https://github.com/nodejs/node/pull/18395
    description: Removed `noAssert` and no implicit coercion of the offset
                 and `byteLength` to `uint32` anymore.
-->

* `offset` {integer} Number of bytes to skip before starting to read. Must
  satisfy `0 <= offset <= buf.length - byteLength`.
* `byteLength` {integer} Number of bytes to read. Must satisfy
  `0 < byteLength <= 6`.
* Returns: {integer}

Reads `byteLength` number of bytes from `buf` at the specified `offset`
and interprets the result as an unsigned integer. Supports up to 48
bits of accuracy.

```js
const buf = Buffer.from([0x12, 0x34, 0x56, 0x78, 0x90, 0xab]);

console.log(buf.readUIntBE(0, 6).toString(16));
// Prints: 1234567890ab
console.log(buf.readUIntLE(0, 6).toString(16));
// Prints: ab9078563412
console.log(buf.readUIntBE(1, 6).toString(16));
// Throws ERR_OUT_OF_RANGE
```

