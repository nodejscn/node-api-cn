<!-- YAML
added: v1.5.0
-->

* `value` {String | Buffer | Integer} What to search for
* `byteOffset` {Integer} Where to begin searching in `buf`. **Default:** `0`
* `encoding` {String} If `value` is a string, this is its encoding.
  **Default:** `'utf8'`
* Returns: {Integer} The index of the first occurrence of `value` in `buf` or `-1`
  if `buf` does not contain `value`

If `value` is:

  * a string, `value` is interpreted according to the character encoding in
    `encoding`.
  * a `Buffer`, `value` will be used in its entirety. To compare a partial
  `Buffer` use [`buf.slice()`].
  * a number, `value` will be interpreted as an unsigned 8-bit integer
  value between `0` and `255`.

Examples:

```js
const buf = Buffer.from('this is a buffer');

// Prints: 0
console.log(buf.indexOf('this')));

// Prints: 2
console.log(buf.indexOf('is'));

// Prints: 8
console.log(buf.indexOf(Buffer.from('a buffer')));

// Prints: 8
// (97 is the decimal ASCII value for 'a')
console.log(buf.indexOf(97));

// Prints: -1
console.log(buf.indexOf(Buffer.from('a buffer example')));

// Prints: 8
console.log(buf.indexOf(Buffer.from('a buffer example').slice(0, 8)));


const utf16Buffer = Buffer.from('\u039a\u0391\u03a3\u03a3\u0395', 'ucs2');

// Prints: 4
console.log(utf16Buffer.indexOf('\u03a3', 0, 'ucs2'));

// Prints: 6
console.log(utf16Buffer.indexOf('\u03a3', -4, 'ucs2'));
```

