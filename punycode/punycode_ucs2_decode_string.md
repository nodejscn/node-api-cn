<!-- YAML
added: v0.7.0
-->

* `string` {string}

`punycode.ucs2.decode()`方法返回一个数组，其中包含字符串中每个Unicode符号的数字代码点值。

```js
punycode.ucs2.decode('abc'); // [0x61, 0x62, 0x63]
// U+1D306四文字符号为中心的代理对：
punycode.ucs2.decode('\uD834\uDF06'); // [0x1D306]
```

