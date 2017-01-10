<!-- YAML
added: v0.1.90
-->

* `target` {Buffer} A `Buffer` to copy into.
* `targetStart` {Integer} The offset within `target` at which to begin
  copying to. **Default:** `0`
* `sourceStart` {Integer} The offset within `buf` at which to begin copying from.
  Ignored when `targetStart` is `undefined`. **Default:** `0`
* `sourceEnd` {Integer} The offset within `buf` at which to stop copying (not
  inclusive). Ignored when `sourceStart` is `undefined`. **Default:** [`buf.length`]
* Returns: {Integer} The number of bytes copied.

Copies data from a region of `buf` to a region in `target` even if the `target`
memory region overlaps with `buf`.

Example: Create two `Buffer` instances, `buf1` and `buf2`, and copy `buf1` from
byte 16 through byte 19 into `buf2`, starting at the 8th byte in `buf2`

```js
const buf1 = Buffer.allocUnsafe(26);
const buf2 = Buffer.allocUnsafe(26).fill('!');

for (let i = 0 ; i < 26 ; i++) {
  // 97 is the decimal ASCII value for 'a'
  buf1[i] = i + 97;
}

buf1.copy(buf2, 8, 16, 20);

// Prints: !!!!!!!!qrst!!!!!!!!!!!!!
console.log(buf2.toString('ascii', 0, 25));
```

Example: Create a single `Buffer` and copy data from one region to an
overlapping region within the same `Buffer`

```js
const buf = Buffer.allocUnsafe(26);

for (var i = 0 ; i < 26 ; i++) {
  // 97 is the decimal ASCII value for 'a'
  buf[i] = i + 97;
}

buf.copy(buf, 0, 4, 10);

// Prints: efghijghijklmnopqrstuvwxyz
console.log(buf.toString());
```

