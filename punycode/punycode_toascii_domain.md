<!-- YAML
added: v0.6.1
-->

* `domain` {string}

`punycode.toASCII()`方法将一个表达国际化域名的Unicode字符串转化为[Punycode][]。只有域名中的非ASCII部分才会被转化。在本身就只含有ASCII字符的字符串上调用`punycode.toASCII()`不会有任何影响。

```js
// 域名编码
punycode.toASCII('mañana.com');  // 'xn--maana-pta.com'
punycode.toASCII('☃-⌘.com');   // 'xn----dqo34k.com'
punycode.toASCII('example.com'); // 'example.com'
```

