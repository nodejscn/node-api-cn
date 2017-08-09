<!-- YAML
added: v0.7.0
-->

* `codePoints` {Array}

`punycode.ucs2.encode()`方法返回一个基于数字代码点值的数组的字符串。

```js
punycode.ucs2.encode([0x61, 0x62, 0x63]); // 'abc'
punycode.ucs2.encode([0x1D306]); // '\uD834\uDF06'
```

