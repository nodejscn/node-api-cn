<!-- YAML
added: v0.11.15
changes:
  - version: v10.0.0
    pr-url: https://github.com/nodejs/node/pull/18395
    description: Removed `noAssert` and no implicit coercion of the offset
                 to `uint32` anymore.
-->

* `value` {number} Number to be written to `buf`.
* `offset` {integer} Number of bytes to skip before starting to write. Must
  satisfy `0 <= offset <= buf.length - 8`.
* Returns: {integer} `offset` plus the number of bytes written.

Writes `value` to `buf` at the specified `offset` with specified endian
format (`writeDoubleBE()` writes big endian, `writeDoubleLE()` writes little
endian). `value` *should* be a valid 64-bit double. Behavior is undefined when
`value` is anything other than a 64-bit double.

```js
const buf = Buffer.allocUnsafe(8);

buf.writeDoubleBE(0xdeadbeefcafebabe, 0);

console.log(buf);
// Prints: <Buffer 43 eb d5 b7 dd f9 5f d7>

buf.writeDoubleLE(0xdeadbeefcafebabe, 0);

console.log(buf);
// Prints: <Buffer d7 5f f9 dd b7 d5 eb 43>
```

