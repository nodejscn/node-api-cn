<!-- YAML
added: v0.7.0
-->

* `string` {string}

The `punycode.ucs2.decode()` method returns an array containing the numeric
codepoint values of each Unicode symbol in the string.

```js
punycode.ucs2.decode('abc'); // [0x61, 0x62, 0x63]
// surrogate pair for U+1D306 tetragram for centre:
punycode.ucs2.decode('\uD834\uDF06'); // [0x1D306]
```

