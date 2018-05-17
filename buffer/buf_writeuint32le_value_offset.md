<!-- YAML
added: v0.5.5
changes:
  - version: v10.0.0
    pr-url: https://github.com/nodejs/node/pull/18395
    description: Removed `noAssert` and no implicit coercion of the offset
                 to `uint32` anymore.
-->

* `value` {integer} Number to be written to `buf`.
* `offset` {integer} Number of bytes to skip before starting to write. Must
  satisfy `0 <= offset <= buf.length - 4`.
* Returns: {integer} `offset` plus the number of bytes written.

Writes `value` to `buf` at the specified `offset` with specified endian
format (`writeUInt32BE()` writes big endian, `writeUInt32LE()` writes little
endian). `value` should be a valid unsigned 32-bit integer. Behavior is
undefined when `value` is anything other than an unsigned 32-bit integer.

```js
const buf = Buffer.allocUnsafe(4);

buf.writeUInt32BE(0xfeedface, 0);

console.log(buf);
// Prints: <Buffer fe ed fa ce>

buf.writeUInt32LE(0xfeedface, 0);

console.log(buf);
// Prints: <Buffer ce fa ed fe>
```

