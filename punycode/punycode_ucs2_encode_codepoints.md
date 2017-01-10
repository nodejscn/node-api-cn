<!-- YAML
added: v0.7.0
-->

* `codePoints` {Array}

The `punycode.ucs2.encode()` method returns a string based on an array of
numeric code point values.

```js
punycode.ucs2.encode([0x61, 0x62, 0x63]); // 'abc'
punycode.ucs2.encode([0x1D306]); // '\uD834\uDF06'
```

