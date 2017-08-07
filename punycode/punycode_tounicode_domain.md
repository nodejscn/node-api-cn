<!-- YAML
added: v0.6.1
-->

* `domain` {string}

`punycode.toUnicode()`方法将一个包含[Punycode][]编码的域名字符串转化为Unicode字符串。只有域名中的[Punycode][]部分才会被转化。

```js
// 域名解码
punycode.toUnicode('xn--maana-pta.com'); // 'mañana.com'
punycode.toUnicode('xn----dqo34k.com');  // '☃-⌘.com'
punycode.toUnicode('example.com');       // 'example.com'
```

