<!-- YAML
added: v0.11.13
-->

* `target` {Buffer} A `Buffer` to compare to
* `targetStart` {Integer} The offset within `target` at which to begin
  comparison. **Default:** `0`
* `targetEnd` {Integer} The offset with `target` at which to end comparison
  (not inclusive). Ignored when `targetStart` is `undefined`.
  **Default:** `target.length`
* `sourceStart` {Integer} The offset within `buf` at which to begin comparison.
  Ignored when `targetStart` is `undefined`. **Default:** `0`
* `sourceEnd` {Integer} The offset within `buf` at which to end comparison
  (not inclusive). Ignored when `targetStart` is `undefined`.
  **Default:** [`buf.length`]
* Returns: {Integer}

Compares `buf` with `target` and returns a number indicating whether `buf`
comes before, after, or is the same as `target` in sort order.
Comparison is based on the actual sequence of bytes in each `Buffer`.

* `0` is returned if `target` is the same as `buf`
* `1` is returned if `target` should come *before* `buf` when sorted.
* `-1` is returned if `target` should come *after* `buf` when sorted.

Examples:

```js
const buf1 = Buffer.from('ABC');
const buf2 = Buffer.from('BCD');
const buf3 = Buffer.from('ABCD');

// Prints: 0
console.log(buf1.compare(buf1));

// Prints: -1
console.log(buf1.compare(buf2));

// Prints: -1
console.log(buf1.compare(buf3));

// Prints: 1
console.log(buf2.compare(buf1));

// Prints: 1
console.log(buf2.compare(buf3));

// Prints: [ <Buffer 41 42 43>, <Buffer 41 42 43 44>, <Buffer 42 43 44> ]
// (This result is equal to: [buf1, buf3, buf2])
console.log([buf1, buf2, buf3].sort(Buffer.compare));
```

The optional `targetStart`, `targetEnd`, `sourceStart`, and `sourceEnd`
arguments can be used to limit the comparison to specific ranges within `target`
and `buf` respectively.

Examples:

```js
const buf1 = Buffer.from([1, 2, 3, 4, 5, 6, 7, 8, 9]);
const buf2 = Buffer.from([5, 6, 7, 8, 9, 1, 2, 3, 4]);

// Prints: 0
console.log(buf1.compare(buf2, 5, 9, 0, 4));

// Prints: -1
console.log(buf1.compare(buf2, 0, 6, 4));

// Prints: 1
console.log(buf1.compare(buf2, 5, 6, 5));
```

A `RangeError` will be thrown if: `targetStart < 0`, `sourceStart < 0`,
`targetEnd > target.byteLength` or `sourceEnd > source.byteLength`.

