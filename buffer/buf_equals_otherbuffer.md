<!-- YAML
added: v0.11.13
-->

* `otherBuffer` {Buffer} A `Buffer` to compare to
* Returns: {Boolean}

Returns `true` if both `buf` and `otherBuffer` have exactly the same bytes,
`false` otherwise.

Examples:

```js
const buf1 = Buffer.from('ABC');
const buf2 = Buffer.from('414243', 'hex');
const buf3 = Buffer.from('ABCD');

// Prints: true
console.log(buf1.equals(buf2));

// Prints: false
console.log(buf1.equals(buf3));
```

