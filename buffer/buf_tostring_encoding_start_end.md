<!-- YAML
added: v0.1.90
-->

* `encoding` {String} The character encoding to decode to. **Default:** `'utf8'`
* `start` {Integer} The byte offset to start decoding at. **Default:** `0`
* `end` {Integer} The byte offset to stop decoding at (not inclusive).
  **Default:** [`buf.length`]
* Returns: {String}

Decodes `buf` to a string according to the specified character encoding in
`encoding`. `start` and `end` may be passed to decode only a subset of `buf`.

Examples:

```js
const buf1 = Buffer.allocUnsafe(26);

for (var i = 0 ; i < 26 ; i++) {
  // 97 is the decimal ASCII value for 'a'
  buf1[i] = i + 97;
}

// Prints: abcdefghijklmnopqrstuvwxyz
console.log(buf1.toString('ascii'));

// Prints: abcde
console.log(buf1.toString('ascii', 0, 5));


const buf2 = Buffer.from('tést');

// Prints: 74c3a97374
console.log(buf2.toString('hex'));

// Prints: té
console.log(buf2.toString('utf8', 0, 3));

// Prints: té
console.log(buf2.toString(undefined, 0, 3));
```

