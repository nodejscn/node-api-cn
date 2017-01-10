<!-- YAML
added: v5.10.0
-->

* Returns: {Buffer} A reference to `buf`

Interprets `buf` as an array of unsigned 16-bit integers and swaps the byte-order
*in-place*. Throws a `RangeError` if [`buf.length`] is not a multiple of 2.

Examples:

```js
const buf1 = Buffer.from([0x1, 0x2, 0x3, 0x4, 0x5, 0x6, 0x7, 0x8]);

// Prints: <Buffer 01 02 03 04 05 06 07 08>
console.log(buf1);

buf1.swap16();

// Prints: <Buffer 02 01 04 03 06 05 08 07>
console.log(buf1);


const buf2 = Buffer.from([0x1, 0x2, 0x3]);

// Throws an exception: RangeError: Buffer size must be a multiple of 16-bits
buf2.swap32();
```

