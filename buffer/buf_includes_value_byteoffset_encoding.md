<!-- YAML
added: v5.3.0
-->

* `value` {String | Buffer | Integer} What to search for
* `byteOffset` {Integer} Where to begin searching in `buf`. **Default:** `0`
* `encoding` {String} If `value` is a string, this is its encoding.
  **Default:** `'utf8'`
* Returns: {Boolean} `true` if `value` was found in `buf`, `false` otherwise

Equivalent to [`buf.indexOf() !== -1`][`buf.indexOf()`].

Examples:

```js
const buf = Buffer.from('this is a buffer');

// Prints: true
console.log(buf.includes('this'));

// Prints: true
console.log(buf.includes('is'));

// Prints: true
console.log(buf.includes(Buffer.from('a buffer')));

// Prints: true
// (97 is the decimal ASCII value for 'a')
console.log(buf.includes(97));

// Prints: false
console.log(buf.includes(Buffer.from('a buffer example')));

// Prints: true
console.log(buf.includes(Buffer.from('a buffer example').slice(0, 8)));

// Prints: false
console.log(buf.includes('this', 4));
```

