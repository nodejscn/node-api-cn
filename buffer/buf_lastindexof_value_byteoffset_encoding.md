<!-- YAML
added: v6.0.0
-->

* `value` {String | Buffer | Integer} What to search for
* `byteOffset` {Integer} Where to begin searching in `buf` (not inclusive).
  **Default:** [`buf.length`]
* `encoding` {String} If `value` is a string, this is its encoding.
  **Default:** `'utf8'`
* Returns: {Integer} The index of the last occurrence of `value` in `buf` or `-1`
  if `buf` does not contain `value`

Identical to [`buf.indexOf()`], except `buf` is searched from back to front
instead of front to back.

Examples:

```js
const buf = Buffer.from('this buffer is a buffer');

// Prints: 0
console.log(buf.lastIndexOf('this'));

// Prints: 17
console.log(buf.lastIndexOf('buffer'));

// Prints: 17
console.log(buf.lastIndexOf(Buffer.from('buffer')));

// Prints: 15
// (97 is the decimal ASCII value for 'a')
console.log(buf.lastIndexOf(97));

// Prints: -1
console.log(buf.lastIndexOf(Buffer.from('yolo')));

// Prints: 5
console.log(buf.lastIndexOf('buffer', 5));

// Prints: -1
console.log(buf.lastIndexOf('buffer', 4));


const utf16Buffer = Buffer.from('\u039a\u0391\u03a3\u03a3\u0395', 'ucs2');

// Prints: 6
console.log(utf16Buffer.lastIndexOf('\u03a3', null, 'ucs2'));

// Prints: 4
console.log(utf16Buffer.lastIndexOf('\u03a3', -5, 'ucs2'));
```

